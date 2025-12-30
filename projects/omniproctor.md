---
layout: default
title: Safe Exam Browser (Omniproctor)
---

# Safe Exam Browser (Omniproctor)

**Repository:** [Vishal490404/Omniproctor](https://github.com/Vishal490404/Omniproctor)

Omniproctor is a secure assessment browser designed to mitigate weaknesses in existing online examination platforms like HackerRank and Hackerearth.

## Architecture

Omniproctor operates on a **Classroom-based model** where teachers create virtual classrooms and students join via invite links. The system complements existing assessment platforms by providing an **OS-level security layer**.

### How it works
1.  **Student Environment**: The student joins a classroom via a web dashboard.
2.  **Secure Browser**: When a test is launched, the Secure Browser App takes over.
3.  **External Link**: It loads the external test link (e.g., HackerRank).
4.  **OS-Level Security**: The browser enforces security by blocking screen sharing, task switching, and unauthorized network access.

[View full Architecture Document](https://github.com/Vishal490404/Omniproctor/blob/main/docs/architecture.md)

## Challenges & Solutions

### Preventing Screen Sharing and Remote Access

**The Problem:**
Preventing users from sharing their screen or using remote desktop tools during exams is difficult. Simply monitoring background processes is ineffective because users can rename files or use advanced tools to hide processes.

**The Solution:**
Instead of blacklisting processes, we **inverted the problem** by controlling network access at the firewall level.
- We implemented an **"allowlist" approach** where only the Omniproctor browser executable is granted internet access.
- All other applications and background processes are blocked from accessing the network.
- This effectively cuts off screen sharing (TeamViewer, Discord, etc.) without needing to identify them individually.

[View full Challenges Document](https://github.com/Vishal490404/Omniproctor/blob/main/docs/project_challenges.md)

[Back to Home](../index.html)
