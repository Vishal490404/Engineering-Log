---
layout: default
title: WhatsApp Bot
---

# Contest-Reminder-WhatsApp-Bot

**Repository:** [Vishal490404/Contest-Reminder-WhatsApp-Bot](https://github.com/Vishal490404/Contest-Reminder-WhatsApp-Bot)

Contest-Reminder-WhatsApp-Bot is an automated WhatsApp notification system designed to keep competitive programmers updated about upcoming coding contests from major platforms like CodeChef, Codeforces, LeetCode, and AtCoder.

## Architecture

The bot automates the process of checking for contests and sending notifications directly to user groups.

### How It Works
1. **Scheduled Jobs**: Uses `node-schedule` to run tasks at specific times.
2. **Data Aggregation**: Fetches contest data from Clist API.
3. **WhatsApp Integration**: Uses `Baileys` library to interact with WhatsApp Web API.

[View full Architecture Document](https://goofball4.readthedocs.io/en/latest/architecture/)

## Challenges & Solutions

### Tracking Multiple Platforms
**The Problem:**
Keeping track of contests across multiple platforms is challenging. Missing contests due to timezone confusion or simply forgetting about them is common.

**The Solution:**
The bot centralizes information by aggregating contest data and provides proactive notifications and smart reminders 30 minutes before each contest.

[View full Challenges Document](https://goofball4.readthedocs.io/en/latest/challenges/)

[Back to Home](../index.html)
