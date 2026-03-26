# Day 2 — System Identification & File System Basics

## Overview
Today I focused on understanding how to identify key system information in Linux and how to navigate and manage the file system. The goal was to build a strong foundation that will support future work in networking and security tools.

## What I worked on

### System Identification
I used commands like `uname -a` and `cat /etc/os-release` to understand the system I am working on.

From this, I learned:
- My system is running Kali Linux (rolling release)
- The kernel version is 6.18.12
- The system is using ARM64 architecture
- The hostname of my machine is "kali"

I also learned the difference between:
- Kernel-level information (`uname -a`)
- OS-level information (`/etc/os-release`)

This helped me understand how to identify a machine during an investigation.

---

### File System Basics
I practiced basic Linux commands to navigate and manage directories and files.

Commands used:
- `mkdir` to create a directory
- `cd` to move between directories
- `touch` to create a file
- `ls` to view the contents of the current directory

I created a folder called `day2_lab` and inside it created a file called `notes.txt` to document my work.

---

## Key Takeaways
- The kernel is the core part of the operating system that interacts with hardware
- System information is important for identifying vulnerabilities and understanding an environment
- Knowing how to navigate the file system is essential for storing and analyzing data during investigations
- Small details (like kernel version and architecture) can have a big impact in cybersecurity

---

## Challenges
- Understanding how to interpret the output of commands like `uname -a`
- Learning the difference between system-level and OS-level information
- Getting comfortable with Linux commands without relying on copy/paste

---

## Reflection
Today was focused on building a foundation rather than rushing through tools. I took time to understand what each command was doing and why it matters in a cybersecurity context. I’m starting to see how these basic skills connect to real-world SOC work.

---

## Next Steps
- Learn how to identify IP addresses and network information
- Practice connectivity testing (ping, DNS vs IP)
- Begin working with tools like Nmap for network scanning
