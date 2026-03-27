# Day 3 — Network Scanning & Subnetting Fundamentals

## Overview
On Day 3, I focused on understanding how devices are identified on a network and how to discover other systems using basic network scanning techniques. This included learning about IP addressing, subnetting, and using Nmap to perform host discovery.

---

## Mission 1 — Identifying My System

I used the following command:

ip a

From this, I identified:
- **IP Address:** 192.168.64.2  
- **Subnet:** /24  
- **Interface:** (varies depending on system, typically eth0 or wlan0)

This helped me understand how my machine is identified within a network.

---

## Mission 2 — Understanding Subnets

I learned that `/24` represents how an IP address is divided between the network and host portions.

- `/24` means:
  - First 24 bits = network
  - Last 8 bits = hosts

From my IP:
192.168.64.2/24

I determined:
- **Network Address:** 192.168.64.0/24  
- **Usable Range:** 192.168.64.1 – 192.168.64.254  
- **Total possible addresses:** 256  
- **Usable devices:** 254  

This showed me how networks are structured and how to determine the correct range to scan.

---

## Mission 3 — Network Scanning with Nmap

I performed a network scan using:

nmap -sn 192.168.64.0/24

### What this did:
- Scanned all possible IP addresses in the network
- Identified which hosts are active

### Results:
- **Total IPs scanned:** 256  
- **Active devices found:** 2  

### Key Insight:
Even though there are 256 possible IP addresses, only a small number of them are actually in use. This reinforced that not every IP in a range corresponds to a real device.

---

## Mission 4 — Key Takeaways

- Subnetting determines how networks are divided and scanned
- `/24` is a common subnet for home and small networks
- Nmap can quickly identify active devices on a network
- Network scanning is a foundational skill in cybersecurity

---

## Why This Matters (Cybersecurity Context)

Network scanning is critical in cybersecurity because it allows analysts to:
- Identify active devices on a network
- Understand the network’s attack surface
- Detect unauthorized or unknown systems
- Begin the process of vulnerability assessment

This is a core skill used in:
- SOC analysis
- Penetration testing
- Incident response

---

## Reflection

Today helped me move beyond just running commands to actually understanding what I am scanning and why. I now have a clearer understanding of how IP addresses, subnetting, and network discovery all connect in a real-world cybersecurity context.