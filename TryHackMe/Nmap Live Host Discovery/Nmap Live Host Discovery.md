 # Nmap Live Host Discovery

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Nmap Live Host Discovery  
**Date Completed:** August 11, 2026  
**Difficulty:** Medium  
**Room Type:** Reading + Hands-on (Nmap Commands)

---

# Objective

The objective of this room was to learn how Nmap discovers live hosts using different host discovery techniques. The room explained how various protocols such as ARP, ICMP, TCP, and UDP can be used to determine whether a system is online and demonstrated when each method is most effective depending on the target environment.

---

# What is Host Discovery?

Host discovery is the process of identifying which devices are online and reachable before performing additional enumeration or port scanning. By discovering live hosts first, penetration testers can focus their efforts on systems that are actually active.

---

# Why Host Discovery Matters

Host discovery is an important first step in a penetration test because scanning offline systems wastes time and creates unnecessary network traffic. Identifying live hosts first makes reconnaissance more efficient and reduces unnecessary scanning.

---

# Networking Concepts

## ARP (Address Resolution Protocol)

- **Layer:** Link Layer (TCP/IP) / Data Link Layer (OSI)
- **Port:** None
- **Purpose:** Maps IP addresses to MAC addresses on the local network.

### Why Penetration Testers Use It

ARP is the fastest and most reliable method for discovering live hosts on the same subnet because devices must respond to ARP requests in order to communicate over Ethernet.

---

## ICMP (Internet Control Message Protocol)

- **Layer:** Network Layer
- **Port:** None
- **Purpose:** Used for diagnostics and network communication.

Common ICMP messages include:

- Echo Request
- Echo Reply
- Timestamp Request
- Address Mask Request

### Why Penetration Testters Use It

ICMP allows penetration testers to determine whether a remote host is reachable before beginning additional enumeration.

---

## TCP

- **Layer:** Transport Layer
- **Connection-Oriented:** Yes

Nmap can use TCP packets such as SYN or ACK packets to determine whether a host is online.

### Why Penetration Testters Use It

TCP discovery is useful when ICMP Echo Requests are filtered or blocked by a firewall.

---

## UDP

- **Layer:** Transport Layer
- **Connection-Oriented:** No

UDP does not establish a connection before sending data.

If a host responds with an ICMP Port Unreachable message, Nmap can determine that the host is alive.

### Why Penetration Testers Use It

UDP discovery provides another alternative when traditional ICMP host discovery is unavailable.

---

# Local Network vs Remote Network

## Same Local Network

Preferred discovery method:

- ARP Scan

Reason:

ARP is faster and more reliable because devices must respond to ARP requests to communicate over Ethernet.

---

## Remote Network

Preferred discovery methods:

- ICMP
- TCP
- UDP

Reason:

ARP does not travel across routers, so Nmap must rely on higher-layer protocols.

---

# Commands Learned

## ARP Scan

```bash
sudo nmap -PR 10.200.6.0/24
```

### Purpose

Uses ARP requests to discover live hosts on the local network.

### Real-World Use

Used when the penetration tester is on the same subnet as the target.

---

## ICMP Echo Scan

```bash
sudo nmap -PE -sn 10.200.6.0/24
```

### Purpose

Uses ICMP Echo Requests to identify live hosts.

### Real-World Use

Useful when scanning hosts outside the local network.

---

## ICMP Timestamp Scan

```bash
sudo nmap -PP -sn 10.200.6.0/24
```

### Purpose

Uses ICMP Timestamp Requests to determine whether a host responds.

### Real-World Use

Provides an alternative discovery method when Echo Requests are filtered.

---

## ICMP Address Mask Scan

```bash
sudo nmap -PM -sn 10.200.6.0/24
```

### Purpose

Uses ICMP Address Mask Requests to determine whether a host is online.

### Real-World Use

Legacy discovery method that may still respond on older systems.

---

## TCP SYN Ping

```bash
sudo nmap -PS22,80,443 -sn 10.200.6.0/30
```

### Purpose

Sends TCP SYN packets to ports 22, 80, and 443.

If a SYN-ACK response is received, the host is considered online.

### Networking Concepts

- Port 22 — SSH
- Port 80 — HTTP
- Port 443 — HTTPS

### Real-World Use

Useful when ICMP Echo Requests are blocked but common TCP services remain accessible.

---

## TCP ACK Ping

```bash
sudo nmap -PA22,80,443 -sn 10.200.6.0/30
```

### Purpose

Sends TCP ACK packets.

If the target replies with an RST packet, the host is considered online.

### Real-World Use

Useful for host discovery through certain firewall configurations.

---

## UDP Ping

```bash
sudo nmap -PU53,161,162 -sn 10.200.6.0/30
```

### Purpose

Sends UDP packets to common UDP services.

If the host replies with an ICMP Port Unreachable message or a UDP response, Nmap can determine the host is online.

### Networking Concepts

- Port 53 — DNS
- Port 161 — SNMP
- Port 162 — SNMP Trap

### Real-World Use

Useful when ICMP Echo Requests are filtered and UDP services are available.

---

# Nmap Host Discovery Logic

Different host discovery methods all attempt to answer the same question:

**"Is this host alive?"**

They simply use different protocols.

| Discovery Method | Protocol Used | Best Situation |
|-----------------|---------------|----------------|
| ARP | ARP | Same Local Network |
| ICMP Echo | ICMP | Remote Networks |
| ICMP Timestamp | ICMP | Alternative ICMP Method |
| ICMP Address Mask | ICMP | Legacy Systems |
| TCP SYN | TCP | ICMP Blocked |
| TCP ACK | TCP | Firewall Evasion |
| UDP Ping | UDP | Alternative Discovery |

---

# What I Learned

This room taught me that Nmap has multiple methods for discovering live hosts instead of relying only on ICMP ping requests. Learning these different discovery techniques helped me understand how Nmap adapts to different network environments and firewall configurations.

I also learned that different protocols can all be used to answer the same question: **Is the host online?**

---

# Real-World Application

During a penetration test, selecting the appropriate host discovery technique depends on the target environment. If the tester is on the same subnet, ARP is usually the fastest option. If scanning a remote network, ICMP, TCP, or UDP discovery techniques may be more appropriate depending on firewall rules and network configuration.

---

# Interview Notes

## What is host discovery?

Host discovery is the process of identifying live systems on a network before beginning enumeration or port scanning.

---

## Why does Nmap perform host discovery first?

Nmap performs host discovery first to avoid scanning offline systems, making the scanning process faster and more efficient.

---

## Why is it important to understand multiple host discovery techniques?

Different organizations configure their networks differently. Some block ICMP, while others may filter TCP or UDP traffic. Understanding multiple host discovery methods allows penetration testers to adapt to different environments and continue gathering information even when one technique fails.

---

## Which discovery method did you find the most useful?

I found ARP discovery the most useful because it is extremely fast and reliable when scanning hosts on the same local network.

---

# Key Takeaway

Host discovery is one of the most important stages of reconnaissance. Understanding how ARP, ICMP, TCP, and UDP discovery techniques work allows penetration testers to efficiently identify live hosts regardless of the network environment or firewall configuration.

---

# Skills Developed

- Nmap Host Discovery
- ARP
- ICMP
- TCP
- UDP
- Network Reconnaissance
- Host Enumeration
- Nmap
- Networking Fundamentals
- Firewall Awareness

---

# Screenshots

This room included both conceptual learning and hands-on Nmap host discovery exercises using multiple protocols.

---

# Personal Reflection

The biggest lesson I learned from this room was that Nmap offers many different host discovery techniques beyond the basic scans I was already familiar with, such as `-sS` and `-sV`. Learning these additional methods showed me how to adapt my reconnaissance depending on the target environment instead of relying on a single approach.

I also learned that understanding multiple host discovery techniques is important because different organizations may block certain protocols or place systems on different network segments. Having multiple discovery methods makes a penetration tester more effective and adaptable.

The ARP discovery method was the most useful to me because it is fast and reliable when operating on the same local network as the target.

This room will help me during future penetration tests because I now understand that there are multiple ways to discover live hosts and that choosing the correct discovery technique depends on the network environment rather than simply running the same scan every time.