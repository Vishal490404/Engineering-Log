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
flowchart LR
    %% Global Graph Settings
    linkStyle default stroke:#d4d4d4,stroke-width:2px,fill:none;

    %% Node Styles
    classDef actor fill:#e1f5fe,stroke:#0277bd,stroke-width:2px,color:#000;
    classDef component fill:#fff9c4,stroke:#fbc02d,stroke-width:2px,color:#000;
    classDef storage fill:#e0f2f1,stroke:#00695c,stroke-width:2px,color:#000;
    classDef database fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#000;
    classDef subgraphStyle fill:none,stroke:#fff,stroke-width:1px,stroke-dasharray: 5 5,color:#fff;

    subgraph Actors ["Users"]
        direction TB
        Instructor([Instructor]):::actor
        Participant([Participant]):::actor
    end
    class Actors subgraphStyle

    subgraph WebLayer ["Management & Web"]
        direction TB
        WebApp["Web App / Backend"]:::component
        DB[("Database")]:::database
    end
    class WebLayer subgraphStyle

    subgraph ExecLayer ["Interactive Execution"]
        direction TB
        JHub["JupyterHub"]:::component
        UserContainer["User Container"]:::component
    end
    class ExecLayer subgraphStyle

    subgraph GradingLayer ["Grading & Async"]
        direction TB
        RabbitMQ["RabbitMQ"]:::component
        Grader["Grading Worker"]:::component
    end
    class GradingLayer subgraphStyle

    subgraph StorageLayer ["Storage"]
        S3[("S3 Bucket")]:::storage
    end
    class StorageLayer subgraphStyle

    %% 1. Setup Flow
    Instructor -->|"1. Create Workshop"| WebApp
    WebApp -.->|"Store Content"| S3

    %% 2. Execution Flow
    Participant -->|"2. Login"| JHub
    JHub -->|"3. Spawn"| UserContainer
    UserContainer -.->|"4. Fetch Files"| S3

    %% 3. Grading Flow
    Participant -->|"5. Submit"| WebApp
    WebApp -->|"6. Queue Job"| RabbitMQ
    RabbitMQ -->|"7. Process"| Grader
    Grader -.->|"8. Fetch Scripts"| S3
    Grader -->|"9. Store Result"| WebApp
    WebApp -->|"10. Update DB"| DB

</div>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true, theme: 'dark' });
</script>

## Detailed Documentation

For a deeper dive into the system's implementation, configuration, and usage, please refer to the full documentation:

<a href="https://drive.google.com/file/d/1NpsIlMhWAU4oKxJHs37bQgkunIDjwYFY/view?usp=sharing" target="_blank" class="btn">📄 View Documentation</a>

[Back to Home](../index.html)
