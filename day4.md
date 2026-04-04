# Day 4 — Packet Capture, ICMP Analysis, and Understanding Network Communication

## Overview

On Day 4, I moved from basic networking concepts into **real network observation** using `tshark`.  
This was my first time actually **seeing packets in real time**, which helped connect theory (IP addresses, protocols) to actual behavior.

The main focus was:
- capturing network traffic
- understanding what a packet is
- analyzing ICMP (ping) communication
- learning how to control and filter packet capture

---

## Step 1 — Identifying My Network Interface

Command used:

```bash
ip a
```

### What this does:
- Displays all network interfaces on the system
- Shows IP addresses assigned to each interface

### Key findings:
- **Interface:** eth0  
- **IP Address:** 192.168.64.2  

### Why this matters:
Before capturing traffic, I need to know:
- which interface traffic is flowing through
- what my system’s identity is on the network

This is critical for:
- packet capture
- network scanning
- investigation context

---

## Step 2 — Capturing Live Traffic with tshark

Command used:

```bash
sudo tshark -i eth0
```

### What this does:
- `sudo` → runs with elevated privileges (required for packet capture)
- `tshark` → command-line packet analyzer (Wireshark CLI version)
- `-i eth0` → captures traffic on the eth0 interface

### What happened:
- The command began capturing packets continuously
- Output showed many lines of network communication
- It did **not stop automatically**

---

## Problem Encountered — tshark Would Not Stop

Initially, `Ctrl + C` did not stop the process.

### Solution:
- Pressed `Ctrl + Z` → paused the process  
- Ran:

```bash
kill %1
```

### Alternative method:
```bash
ps aux | grep tshark
kill -9 <PID>
```

### What I learned:
- How to manage and terminate running processes  
- That some tools require manual control in Linux environments  

---

## Fix — Limiting Packet Capture

Command used:

```bash
sudo tshark -i eth0 -c 20
```

### What this does:
- `-c 20` → captures only 20 packets, then stops automatically

### Why this matters:
- prevents infinite capture  
- makes output easier to analyze  
- improves workflow efficiency  

---

## Understanding What a Packet Is

Before this lab, I did not fully understand what a packet actually was.

### Definition:
A **packet** is a small unit of data sent between devices over a network.

### Analogy:
Sending data is like shipping packages:
- large message = broken into smaller pieces (packets)
- each packet contains:
  - source (who sent it)
  - destination (where it’s going)
  - protocol (type of communication)
  - part of the data

---

## Observing Background Traffic

Initial capture showed:
- router broadcasts  
- multicast traffic  
- IPv6 communication  

### Insight:
Even when I am not actively doing anything, the network is:
- constantly communicating  
- maintaining connections  
- exchanging control information  

This showed me that:
> networks are never truly “idle”

---

## Step 3 — Generating My Own Traffic

Command used:

```bash
ping google.com
```

### What this does:
- Sends ICMP echo requests to Google  
- Waits for replies  

### Important concept:
Before sending packets, DNS resolves:

```
google.com → 142.250.191.14
```

This showed me:
- domain names are human-readable  
- IP addresses are what computers actually use  

---

## Capturing ICMP Traffic

Command used:

```bash
sudo tshark -i eth0 -c 20
```

### What I observed:
- packets going from my machine → Google  
- packets returning from Google → my machine  

Example:

```
192.168.64.2 → 142.250.191.14 ICMP Echo request  
142.250.191.14 → 192.168.64.2 ICMP Echo reply
```

---

## Step 4 — Filtering Only ICMP Traffic

Initial mistake:

```bash
sudo tshark -i eth0 icmp -c 10
```

### Error:
`tshark: Invalid capture filter`

### Fix:

```bash
sudo tshark -i eth0 -f "icmp" -c 10
```

### What I learned:
- `-f` is required for capture filters  
- commands have strict syntax  
- troubleshooting is part of the learning process  

---

## ICMP Analysis — Understanding the Output

### Example packet pair:

```
192.168.64.2 → 142.250.191.14 ICMP Echo request  
142.250.191.14 → 192.168.64.2 ICMP Echo reply
```

### Breakdown:
- `192.168.64.2` = my machine  
- `142.250.191.14` = Google server  
- `ICMP` = protocol used for ping  
- `Echo request` = outgoing packet  
- `Echo reply` = incoming response  

---

## Key Pattern Observed

```
request → reply  
request → reply  
request → reply  
```

### Meaning:
- communication is working normally  
- responses match requests  

---

## TTL (Time To Live)

Observed:
- my packets: `ttl=64`  
- Google’s packets: `ttl=117`  

### What this means:
- packets travel through multiple devices (routers)  
- TTL decreases as packets move  
- helps estimate distance and path  

---

## SOC Analyst Thinking

Instead of just reading packets, I practiced thinking like an analyst:

Questions I asked:
- Who initiated the communication?  
- Where is it going?  
- Is the response expected?  
- Does anything look abnormal?  

### Conclusion:

```
Normal ICMP traffic (benign)
```

---

## MITM vs DNS Spoofing (Concept Learned)

- MITM (ARP spoofing):
  - IP may look normal  
  - attacker is hidden in the middle  

- DNS spoofing:
  - IP changes  
  - traffic is redirected  

Example:

Normal:
```
google.com → 142.250.191.14
```

Spoofed:
```
google.com → attacker IP
```

---

## What I Learned

- How to capture packets using tshark  
- Difference between Wireshark (GUI) and tshark (CLI)  
- How to stop and control long-running processes  
- What a packet is and how data moves across a network  
- How to identify request vs response traffic  
- How DNS resolution works  
- How to filter traffic using capture filters  
- How attackers can manipulate network communication  

---

## Why This Matters

Packet analysis is used to:
- detect suspicious activity  
- investigate incidents  
- trace communication between systems  
- identify attacks  

---

## Reflection

This lab helped me transition from:
- learning commands  
to  
- understanding real network behavior  

I also learned that confusion is part of the process:
- command syntax errors  
- misunderstanding filters  
- not knowing what packets were  

Working through those issues helped deepen my understanding.

---

## Key Takeaway


- A packet is a small unit of communication between devices,
and analyzing packets allows us to understand how systems interact on a network.
- ICMP (Internet Control Message Protocol) is used for network diagnostics and communication between devices, rather than transferring actual data. It allows systems to check connectivity (like with ping) and report errors in the network. By analyzing ICMP traffic, I can determine whether devices are reachable, observe request and reply patterns, and begin identifying normal vs suspicious network behavior.