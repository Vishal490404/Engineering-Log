---
layout: default
title: WARGAMES
---

# WARGAMES

**Repository:** [Walchand-Linux-Users-Group/WARGAMES_2k24](https://github.com/Walchand-Linux-Users-Group/WARGAMES_2k24)

WARGAMES is a terminal-based interactive game with intuitive controls and progressive difficulty levels. It is containerized for easy deployment and safety.

## Architecture

WARGAMES is a standalone, containerized Capture The Flag (CTF) game designed to run locally on the user's machine. It operates entirely via a shell script and Docker containers, ensuring isolation and safety.

### Core Components
- **Start Script**: The entry point for the user.
- **Docker Containers**: Each level runs in an isolated container.
- **GHCR**: Images are pulled from the GitHub Container Registry.

The user executes the start script, which pulls the necessary images and spawns a level container. The user solves the challenge in this isolated environment to get the password for the next level.

[View full Architecture Document](https://github.com/Walchand-Linux-Users-Group/WARGAMES_2k24/blob/master/docs/architecture.md)

## Challenges & Solutions

One of the main challenges was ensuring the game was accessible yet secure. By using Docker, we ensured that even if a user "breaks" the game environment, their host machine remains safe.

[View full Challenges Document](https://github.com/Walchand-Linux-Users-Group/WARGAMES_2k24/blob/master/docs/project_challenges.md)

[Back to Home](../index.html)
