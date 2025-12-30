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

<div class="mermaid">
graph TD
    subgraph "Management & Frontend"
        Instructor[Instructor]
        Participant[Participant]
        WebApp[Web App / Backend]
        DB[(Database)]
    end

    subgraph "Storage"
        S3[S3 Bucket]
    end

    subgraph "Interactive Environment"
        JHub[JupyterHub]
        UserContainer[User Docker Container]
    end

    subgraph "Grading Service"
        RabbitMQ[RabbitMQ]
        Grader[Grading Worker (Docker)]
    end

    %% Workshop Setup
    Instructor -->|1. Create Workshop & Upload Content| WebApp
    WebApp -->|Store Notebooks & Eval Scripts| S3
    Instructor -->|2. Add Participants| WebApp

    %% User Flow
    Participant -->|3. Login| JHub
    JHub -->|Spawn| UserContainer
    Participant -->|4. Run 'start' command| UserContainer
    UserContainer -->|Fetch Workshop Files| S3
    
    %% Grading Flow
    Participant -->|5. Submit Assignment| WebApp
    WebApp -->|6. Queue Job| RabbitMQ
    RabbitMQ -->|7. Process Job| Grader
    Grader -->|Fetch User Code & Eval Script| S3
    Grader -->|8. Evaluate (Output/Time)| Grader
    Grader -->|9. Store Result| WebApp
    WebApp -->|Update Progress| DB

    %% Completion
    Participant -->|10. View Progress & Download Certificate| WebApp
</div>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true });
</script>

[Back to Home](../index.html)
