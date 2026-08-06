 # Active Reconnaissance

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Active Reconnaissance  
**Date Completed:** August 5, 2026  
**Difficulty:** Easy  
**Room Type:** Concept + Command Demonstrations

---

# Objective

The objective of this room was to introduce active reconnaissance, explain its advantages and disadvantages, and demonstrate common tools and commands used to directly interact with a target during the reconnaissance phase, including `ping`, `traceroute`, `telnet`, and `netcat`.

---

# What is Active Reconnaissance?

Active reconnaissance is the process of gathering information about a target by directly interacting with its systems, such as its network, web servers, or other services. Because the target is contacted directly, active reconnaissance is more likely to be detected than passive reconnaissance.

The goal is to collect accurate, real-time technical information that will assist with the penetration test.

---

# Active vs. Passive Reconnaissance

## Active Reconnaissance

Active reconnaissance involves directly communicating with a target to gather information. This includes activities such as host discovery, port scanning, service enumeration, and network analysis.

Because the target is being contacted directly, active reconnaissance creates network traffic that may be detected by firewalls, Intrusion Detection Systems (IDS), Intrusion Prevention Systems (IPS), or security analysts.

---

## Passive Reconnaissance

Passive reconnaissance gathers information without directly interacting with the target. Instead, penetration testers use publicly available resources such as DNS records, WHOIS information, search engines, and OSINT tools to collect intelligence while remaining undetected.

---

# Advantages of Active Reconnaissance

- Provides accurate real-time information
- Identifies live hosts
- Discovers open ports
- Identifies running services
- Helps build an accurate picture of the target's infrastructure
- Allows penetration testers to validate information gathered during passive reconnaissance

---

# Disadvantages of Active Reconnaissance

- Generates network traffic
- Can trigger IDS/IPS alerts
- May be logged by the target organization
- Increases the likelihood of detection
- Must always remain within the authorized scope of the engagement

---

# Commands Learned

## ping -c <IP Address>

### Purpose

Sends ICMP Echo Request packets to determine whether a host is reachable.

### Information Gathered

- Whether the host is online
- Network latency
- Packet loss

### Real-World Use

Penetration testers use `ping` to determine whether a target host is reachable before performing additional reconnaissance or enumeration.

---

## traceroute

### Purpose

Displays the network path packets take from the attacker's machine to the destination.

### Information Gathered

- Network path
- Intermediate routers (hops)
- Response times
- Routing information

### Real-World Use

Traceroute helps penetration testers understand the network topology, identify routing paths, troubleshoot connectivity issues, and gain a better understanding of the target's infrastructure before continuing with additional reconnaissance.

---

## telnet

### Purpose

Creates a TCP connection to a remote service.

### Information Gathered

- Whether a TCP port is open
- Whether a service is responding

### Real-World Use

Although Telnet is no longer recommended for remote administration because it transmits data in plain text, penetration testers can use it to test connectivity to TCP services and verify whether specific ports are accepting connections.

---

## nc (Netcat)

### Purpose

A versatile networking utility used to create connections, listen on ports, transfer files, and communicate with network services.

### Information Gathered

- Service responses
- Open ports
- Network connectivity

### Real-World Use

Netcat is often called the "Swiss Army Knife of Networking." During penetration tests it can be used to:

- Test network connectivity
- Listen for incoming connections
- Receive reverse shells
- Transfer files
- Troubleshoot services
- Connect directly to network services

---

# What I Learned

This room taught me that active reconnaissance provides valuable real-time information directly from the target. While passive reconnaissance is useful for gathering publicly available information, active reconnaissance allows penetration testers to verify hosts, discover running services, and better understand the target's infrastructure.

I also learned that active reconnaissance must always be performed within the authorized scope because it creates network traffic that can be detected.

---

# Real-World Application

During a real penetration test, active reconnaissance is performed after passive reconnaissance has been completed. The information gathered helps penetration testers identify live systems, discover open ports, enumerate services, and better understand the target environment before moving into vulnerability analysis and exploitation.

---

# Interview Notes

## What is active reconnaissance?

Active reconnaissance is the process of gathering information about a target by directly interacting with its systems. It provides accurate, real-time technical information but increases the likelihood of detection because the target receives the traffic.

---

## Why is active reconnaissance important?

Active reconnaissance is important because it provides real-time technical information directly from the target. It allows penetration testers to identify live hosts, open ports, running services, and other information needed to perform an effective security assessment.

---

## When would you choose passive reconnaissance instead?

Passive reconnaissance should be used when gathering information without alerting the target is important. Since it relies on publicly available information, it minimizes the chance of detection while still providing valuable intelligence.

---

## Which command from this room did you find the most useful?

I found `traceroute` the most useful because it helps me understand how traffic reaches the target and provides insight into the network topology. Understanding the network path helps me better analyze the environment before continuing with additional reconnaissance.

---

# Key Takeaway

Active reconnaissance builds upon passive reconnaissance by directly interacting with the target to collect accurate technical information. Understanding when and how to perform active reconnaissance allows penetration testers to gather valuable intelligence while balancing the increased risk of detection.

---

# Skills Developed

- Active Reconnaissance
- Network Discovery
- Host Discovery
- Network Topology Analysis
- ping
- traceroute
- telnet
- Netcat
- Reconnaissance Methodology

---

# Screenshots

This room primarily consisted of learning concepts and practicing networking commands. No exploitation or privilege escalation activities were performed.

---

# Personal Reflection

Learning active reconnaissance will help me become a better penetration tester because it allows me to better understand a target's infrastructure through direct interaction. Learning different reconnaissance techniques will help me identify potential attack surfaces, gather information for later phases of an assessment, and develop multiple approaches when investigating a target.

I would recommend this room to anyone learning penetration testing because active reconnaissance is a fundamental skill that every aspiring penetration tester should understand. The room teaches the basic networking techniques and tools that provide the foundation for more advanced penetration testing activities later in the learning path.