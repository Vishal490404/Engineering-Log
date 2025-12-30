---
layout: default
title: HPC Grading Service
---

# HPC Grading Service - National Supercomputing Mission

This project is a comprehensive platform designed to facilitate workshops on High Performance Computing (HPC) technologies like OpenMP, MPI, and CUDA. It provides an integrated environment for learning, practice, and automated assessment.

## Architecture

The system is built around a central Web Application that manages workshops, users, and content, integrated with a JupyterHub environment for hands-on practice and a scalable grading system for automated evaluation.

### Workflow Overview

1.  **Workshop Management**:
    *   Instructors create workshops and manage participants (via CSV or direct enrollment).
    *   Course content (Jupyter Notebooks) and evaluation scripts are uploaded to an **S3 Bucket**.

2.  **User Environment (JupyterHub)**:
    *   Participants log in to **JupyterHub**, which uses **DockerSpawner** to provision isolated containers.
    *   A custom `start` command inside the terminal fetches the specific workshop content from S3, backing up any previous progress.

3.  **Automated Grading**:
    *   Assignments are submitted for evaluation.
    *   The backend pushes grading tasks to a **RabbitMQ** queue.
    *   **Dockerized Evaluation Environments** pick up tasks, run the user's code against the instructor's evaluation script (checking output correctness and execution time), and report results back to the backend.

4.  **Progress & Certification**:
    *   Participants track their progress on the Web App.
    *   Upon completing all requirements, the system automatically generates a downloadable certificate.

### System Diagram

<div class="mermaid" style="text-align: center;">
flowchart TD
    %% Node Styles
    classDef actor fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:black;
    classDef component fill:#fff9c4,stroke:#fbc02d,stroke-width:2px,color:black;
    classDef storage fill:#e0f2f1,stroke:#00695c,stroke-width:2px,color:black;
    classDef database fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:black;

    subgraph MF ["Management & Frontend"]
        direction TB
        Instructor([Instructor]):::actor
        Participant([Participant]):::actor
        WebApp["Web App / Backend"]:::component
        DB[("Database")]:::database
    end

    subgraph IE ["Interactive Environment"]
        direction TB
        JHub["JupyterHub"]:::component
        UserContainer["User Docker Container"]:::component
    end

    subgraph GS ["Grading Service"]
        direction TB
        RabbitMQ["RabbitMQ"]:::component
        Grader["Grading Worker (Docker)"]:::component
    end

    subgraph Store ["Storage"]
        S3[("S3 Bucket")]:::storage
    end

    %% Workshop Setup
    Instructor -->|"1. Create Workshop & Upload Content"| WebApp
    WebApp -.->|"Store Notebooks & Eval Scripts"| S3
    Instructor -->|"2. Add Participants"| WebApp

    %% User Flow
    Participant -->|"3. Login"| JHub
    JHub -->|"Spawn"| UserContainer
    Participant -->|"4. Run 'start' command"| UserContainer
    UserContainer -.->|"Fetch Workshop Files"| S3
    
    %% Grading Flow
    Participant -->|"5. Submit Assignment"| WebApp
    WebApp -->|"6. Queue Job"| RabbitMQ
    RabbitMQ -->|"7. Process Job"| Grader
    Grader -.->|"Fetch User Code & Eval Script"| S3
    Grader -->|"8. Evaluate"| Grader
    Grader -->|"9. Store Result"| WebApp
    WebApp -->|"Update Progress"| DB

    %% Completion
    Participant -->|"10. View Progress & Download Certificate"| WebApp
</div>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true });
</script>

[Back to Home](../index.html)
