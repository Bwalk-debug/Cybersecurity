 # Nmap Basic Port Scans

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Nmap Basic Port Scans  
**Date Completed:** August 12, 2026  
**Difficulty:** Easy  
**Room Type:** Reading + Command Demonstrations

---

# Objective

The objective of this room was to learn how to perform basic port scanning with Nmap, understand the differences between common scan types, and identify open ports and the services running on a target system.

---

# What is Port Scanning?

Port scanning is the process of probing a target's ports to determine whether they are open, closed, or filtered. The goal is to identify services running on a target so they can be further enumerated for vulnerabilities and possible exploitation.

---

# Why Port Scanning Matters

Port scanning is one of the first stages after host discovery. Once a live host has been identified, port scanning allows a penetration tester to discover what services are exposed to the network. These services can then be enumerated to identify versions, research vulnerabilities, and determine possible attack vectors.

**Reconnaissance Workflow**

```
Host Discovery
        ↓
Port Scanning
        ↓
Service Enumeration
        ↓
Version Detection
        ↓
Vulnerability Analysis
        ↓
Exploitation
```

---

# Networking Concepts

## TCP

- **Layer:** Transport Layer
- **Connection-Oriented:** Yes
- **Uses:** Three-Way Handshake
- **Reliable:** Yes

TCP establishes a connection before transmitting data, making it reliable but slightly slower than UDP.

### Common TCP Services

| Port | Service |
|------|----------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |

---

## UDP

- **Layer:** Transport Layer
- **Connection-Oriented:** No
- **Handshake:** None
- **Reliable:** No

UDP sends data without establishing a connection, making it faster but less reliable than TCP.

### Common UDP Services

| Port | Service |
|------|----------|
| 53 | DNS |
| 67/68 | DHCP |
| 69 | TFTP |
| 123 | NTP |
| 161 | SNMP |
| 162 | SNMP Trap |

---

# Port States

## Open

An **open** port means a service is actively listening and accepting incoming connections.

Example:

```
22/tcp open ssh
```

---

## Closed

A **closed** port means the host is reachable, but no service is listening on that port.

Example:

```
80/tcp closed
```

---

## Filtered

A **filtered** port means Nmap cannot determine whether the port is open because a firewall or filtering device is blocking the probes.

Possible causes include:

- Firewalls
- Router ACLs
- Intrusion Prevention Systems (IPS)
- Security Groups
- Packet Filtering

---

# Commands Learned

## TCP Connect Scan

```bash
nmap -sT <IP Address>
```

### Purpose

Performs a full TCP three-way handshake with the target.

### Packet Exchange

```
SYN
↓
SYN-ACK
↓
ACK
```

The connection is fully established before Nmap closes it.

### Networking Concepts

- Protocol: TCP
- Layer: Transport Layer
- Full TCP Connection

### Why a Penetration Tester Uses It

A penetration tester may choose a TCP Connect Scan when they do not have root or sudo privileges because it uses the operating system's networking stack. Although it is more likely to be logged than a SYN scan, it remains an effective way to identify open ports.

### Limitations

- More likely to be logged
- Generates more network traffic
- Slower than a SYN Scan

---

## TCP SYN Scan

```bash
sudo nmap -sS <IP Address>
```

### Purpose

Performs a half-open scan by sending a SYN packet without completing the TCP three-way handshake.

### Packet Exchange

```
SYN
↓
SYN-ACK
↓
RST
```

The connection is reset before it is fully established.

### Networking Concepts

- Protocol: TCP
- Layer: Transport Layer
- Half-Open Scan

### Why a Penetration Tester Uses It

A TCP SYN Scan is one of the most common scans used during penetration tests because it is fast and generally less likely to be logged than a TCP Connect Scan while still identifying open ports.

### Limitations

- Requires root/sudo privileges
- Can still be detected by IDS/IPS
- May be blocked by firewalls

---

## UDP Scan

```bash
sudo nmap -sU <IP Address>
```

### Purpose

Scans UDP ports to identify UDP services.

### Possible Responses

- UDP Response → Port Open
- ICMP Port Unreachable → Port Closed
- No Response → Open | Filtered

### Networking Concepts

- Protocol: UDP
- Layer: Transport Layer
- Connectionless Communication

### Why a Penetration Tester Uses It

UDP scans help identify services such as DNS, DHCP, SNMP, and other UDP-based applications that may not appear during TCP scans.

### Limitations

- Slower than TCP scanning
- Many UDP services do not respond
- Results often appear as **Open | Filtered**
- Firewalls frequently block UDP traffic

---

# Scan Comparison

| Scan | Advantages | Limitations |
|-------|------------|-------------|
| TCP Connect (-sT) | No root privileges required | More likely to be logged |
| TCP SYN (-sS) | Fast, generally less likely to be logged | Requires root/sudo, can still be detected |
| UDP (-sU) | Finds UDP services | Slow and sometimes inconclusive |

---

# What I Learned

This room taught me that there are multiple ways to perform port scans depending on the situation. Instead of relying on one scan type, penetration testers should understand when each scan is appropriate based on network configuration, firewall rules, and assessment objectives.

I also learned that understanding how TCP and UDP behave helps explain why different scan types produce different results.

---

# Real-World Application

After discovering a live host, a penetration tester performs port scanning to identify exposed services. Once open ports are identified, the tester can enumerate the services, determine software versions, research known vulnerabilities, and decide which attack vectors should be investigated further.

---

# Interview Notes

## What is a port scan?

A port scan is the process of identifying open, closed, or filtered ports on a target system to determine which services are available for further enumeration.

---

## Why is port scanning important?

Port scanning identifies exposed services on a target. Those services can then be enumerated to identify versions, research vulnerabilities, and determine potential attack paths.

---

## Why should a penetration tester understand multiple scan types?

Different organizations configure their networks differently. Some scan types may be blocked or filtered, so understanding multiple techniques allows a penetration tester to adapt to different environments and continue gathering information.

---

## Why is a TCP SYN Scan generally less likely to be logged?

A TCP SYN Scan does not complete the TCP three-way handshake. After receiving a SYN-ACK response, Nmap sends an RST packet instead of the final ACK, meaning the connection is never fully established. Because of this, many applications generate fewer logs than they would for a full TCP Connect Scan.

---

## Why would you choose a TCP Connect Scan instead of a TCP SYN Scan?

A TCP Connect Scan is useful when root or sudo privileges are unavailable because it relies on the operating system's networking stack to establish a full TCP connection.

---

## Which scan did you find the most useful?

The TCP SYN Scan was the most useful because it performs a half-open connection, making it faster and generally less likely to be logged than a TCP Connect Scan while still identifying open ports.

---

# Key Takeaway

Port scanning is the bridge between host discovery and service enumeration. Understanding how different scan types work allows penetration testers to choose the most appropriate technique for a given environment while efficiently identifying exposed services.

---

# Skills Developed

- Nmap
- TCP Connect Scan
- TCP SYN Scan
- UDP Scan
- Port Scanning
- TCP Networking
- UDP Networking
- Network Enumeration
- Service Discovery
- Reconnaissance Methodology

---

# Screenshots

This room focused on learning Nmap scan types and understanding how different TCP and UDP scans work. No screenshots were necessary because the emphasis was on understanding networking concepts and scan behavior rather than demonstrating exploitation or capturing evidence from a target system.

---

# Personal Reflection

The biggest lesson I learned from this room was that I should not rely on a single scan type. Different environments require different approaches, so understanding multiple scanning techniques makes me a more effective penetration tester.

I also learned that organizations may block or filter certain scan types, making it important to understand alternative methods for identifying open ports.

The TCP SYN Scan stood out the most because it performs a half-open connection, allowing a penetration tester to efficiently identify open ports while generating less network traffic than a full TCP Connect Scan.

This room will help me during future penetration tests because I now understand that choosing the correct scan type depends on the target environment rather than always using the same command. Knowing when and why to use each scan will make my reconnaissance more efficient and adaptable.