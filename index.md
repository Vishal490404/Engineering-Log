---
layout: default
title: Home
---

<style>
    .intro-section {
        margin-bottom: 3rem;
        border-bottom: 1px solid #333;
        padding-bottom: 2rem;
    }
    .project-grid {
        display: flex;
        flex-direction: column;
        gap: 2rem;
    }
    .project-card {
        background-color: #0d1117; /* Dark terminal bg */
        border: 1px solid #30363d;
        border-left: 4px solid #2ea043; /* Git green accent */
        padding: 1.5rem;
        border-radius: 6px;
        transition: all 0.2s ease;
    }
    .project-card:hover {
        border-color: #58a6ff;
        border-left-color: #58a6ff;
        transform: translateX(4px);
    }
    .project-header {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        margin-bottom: 0.5rem;
    }
    .project-title {
        margin: 0;
        font-size: 1.5rem;
        font-weight: 600;
        color: #c9d1d9;
    }
    .project-title a {
        text-decoration: none;
        color: inherit;
    }
    .project-summary {
        color: #8b949e;
        font-size: 1rem;
        line-height: 1.6;
        margin-bottom: 1rem;
    }
    .tech-stack {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
        margin-bottom: 1.2rem;
    }
    .tech-tag {
        font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
        font-size: 0.75rem;
        padding: 2px 8px;
        background-color: #161b22;
        border: 1px solid #30363d;
        border-radius: 12px;
        color: #58a6ff;
    }
    .cta-link {
        display: inline-flex;
        align-items: center;
        font-family: 'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, monospace;
        font-size: 0.9rem;
        color: #2ea043;
        text-decoration: none;
        font-weight: 600;
    }
    .cta-link:hover {
        text-decoration: underline;
    }
</style>

<div class="intro-section">
    <h1>Welcome to My Portfolio</h1>
    <p>Hello! I'm <strong>Vishal</strong>. I am a backend-focused engineer passionate about understanding and implementing backend systems.</p>
    <p>I have a keen interest in reverse engineering, bug hunting, and cloud technologies. I play CTF's (a lot of them). This blog documents the technical details, architecture, and challenges I faced while building my projects.</p>
</div>

<h2>Featured Projects</h2>

<div class="project-grid">

    <!-- Project 1: Omniproctor -->
    <div class="project-card">
        <div class="project-header">
            <h3 class="project-title"><a href="./projects/omniproctor.html">Safe Exam Browser (Omniproctor)</a></h3>
        </div>
        <div class="tech-stack">
            <span class="tech-tag">Security</span>
            <span class="tech-tag">PyQt</span>
            <span class="tech-tag">System Hardening</span>
        </div>
        <p class="project-summary">
            A secure assessment browser designed to mitigate weaknesses in existing online examination platforms like HackerRank and Hackerearth. Prevents VM usage, screen sharing, and unauthorized peripherals.
        </p>
        <a href="./projects/omniproctor.html" class="cta-link">View Architecture & Challenges &rarr;</a>
    </div>

    <!-- Project 2: WARGAMES -->
    <div class="project-card">
        <div class="project-header">
            <h3 class="project-title"><a href="./projects/wargames.html">WARGAMES</a></h3>
        </div>
        <div class="tech-stack">
            <span class="tech-tag">Docker</span>
            <span class="tech-tag">Linux</span>
        </div>
        <p class="project-summary">
            A terminal-based interactive game running in isolated Docker containers. Features intuitive controls and progressive difficulty levels. Successfully played by 250+ users during the event.
        </p>
        <a href="./projects/wargames.html" class="cta-link">View Architecture & Challenges &rarr;</a>
    </div>

    <!-- Project 3: WhatsApp Bot -->
    <div class="project-card">
        <div class="project-header">
            <h3 class="project-title"><a href="./projects/whatsapp-bot.html">Contest Reminder Bot</a></h3>
        </div>
        <div class="tech-stack">
            <span class="tech-tag">Automation</span>
            <span class="tech-tag">WhatsApp API</span>
            <span class="tech-tag">Cloud</span>
        </div>
        <p class="project-summary">
            An automated notification system keeping competitive programmers updated about upcoming contests. Aggregates data from CodeChef, Codeforces, LeetCode, and AtCoder.
        </p>
        <a href="./projects/whatsapp-bot.html" class="cta-link">View Architecture & Challenges &rarr;</a>
    </div>

    <!-- Project 4: HPC Grading Service -->
    <div class="project-card">
        <div class="project-header">
            <h3 class="project-title"><a href="./projects/grading-server.html">HPC Grading Service</a></h3>
        </div>
        <div class="tech-stack">
            <span class="tech-tag">HPC</span>
            <span class="tech-tag">JupyterHub</span>
            <span class="tech-tag">RabbitMQ</span>
            <span class="tech-tag">Docker</span>
        </div>
        <p class="project-summary">
            A comprehensive platform for High Performance Computing workshops. Features an integrated environment for learning (JupyterHub), practice, and automated assessment of OpenMP/MPI/CUDA code.
        </p>
        <a href="./projects/grading-server.html" class="cta-link">View Architecture & Challenges &rarr;</a>
    </div>

    <!-- Project 5: Deep Learning Server -->
    <div class="project-card">
        <div class="project-header">
            <h3 class="project-title"><a href="./projects/deep-learning-server.html">Deep Learning Server Setup</a></h3>
        </div>
        <div class="tech-stack">
            <span class="tech-tag">Infrastructure</span>
            <span class="tech-tag">CUDA</span>
            <span class="tech-tag">LLM Ops</span>
        </div>
        <p class="project-summary">
            A high-performance deep learning server setup capable of running LLM workloads. Configured with multi-user JupyterHub access and optimized CUDA environments.
        </p>
        <a href="./projects/deep-learning-server.html" class="cta-link">View Architecture & Challenges &rarr;</a>
    </div>

</div>