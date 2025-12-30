---
layout: default
title: Deep Learning Server Setup
---

# Deep Learning Server Setup

**Repository:** [Vishal490404/Deep-Learning-Server-Setup](https://github.com/Vishal490404/Deep-Learning-Server-Setup)

This project involved setting up a high-performance deep learning server capable of running LLM workloads.

## Architecture & Setup

The server runs **Ubuntu 22.04** and is configured to support **OpenMPI**, **OpenMP**, and **CUDA**.

### Solution: JupyterHub with DockerSpawner

To meet the requirements, we set up a **JupyterHub** instance using **DockerSpawner**.

- **Isolation**: Each user runs in their own isolated Docker container.
- **GPU Support**: The setup includes full support for GPU acceleration (CUDA).
- **Consistency**: Every user starts with the same environment.

### Build Process
1.  Download the NVIDIA HPC SDK driver.
2.  Build the Docker image incorporating the driver.
3.  Configure JupyterHub to spawn containers using this image.

[View full Documentation](https://github.com/Vishal490404/Deep-Learning-Server-Setup/blob/master/docs/index.md)

## Challenges & Solutions

### Resource Management
One of the main challenges is resource allocation.
- **Storage Limits**: Currently, there is no mechanism to limit storage per user.
- **Quotas**: Every user gets a default of 1 CPU and 2 GB RAM.

We are working on ways to provide custom memory and CPU allocations.

[View full Challenges Document](https://github.com/Vishal490404/Deep-Learning-Server-Setup/blob/master/docs/project_challenges.md)

[Back to Home](../index.html)
