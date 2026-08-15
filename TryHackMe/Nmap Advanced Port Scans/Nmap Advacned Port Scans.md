 # Nmap Advanced Port Scans

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Nmap Advanced Port Scans  
**Date Completed:** August 14, 2026  
**Difficulty:** Medium  
**Room Type:** Reading + Nmap Command Demonstrations

---

# Objective

The objective of this room was to learn advanced Nmap scanning techniques, understand how different scan types interact with firewalls and intrusion detection systems (IDS), and determine which scans are more effective depending on a target's security configuration.

---

# Why Advanced Port Scans Matter

Basic scans such as TCP SYN and TCP Connect are effective in many environments, but modern networks often use firewalls and intrusion detection systems to monitor or filter traffic.

Advanced scan types use different TCP flag combinations and scanning techniques to gather information about a target while adapting to different firewall configurations.

---

# Networking Concepts

## Firewall

A firewall is a security device or software that monitors and filters incoming and outgoing network traffic based on predefined security rules.

Its primary purpose is to:

- Allow legitimate traffic
- Block unauthorized traffic
- Enforce network security policies

---

## Intrusion Detection System (IDS)

An IDS monitors network traffic for suspicious activity and generates alerts when potential attacks are detected.

Unlike a firewall, an IDS normally does not block traffic.

---

## Firewall vs IDS

| Firewall | IDS |
|----------|-----|
| Blocks or allows traffic | Detects suspicious activity |
| Uses security rules | Monitors network behavior |
| Prevents unauthorized access | Generates alerts |
| Active protection | Passive monitoring |

---

# TCP Flag Scans

Many advanced scans rely on different TCP flag combinations.

Common TCP Flags:

- SYN
- ACK
- FIN
- PSH
- URG
- RST

Different combinations cause operating systems and firewalls to respond differently.

---

# Commands Learned

## TCP NULL Scan

```bash
sudo nmap -sN <IP Address>
```

### Purpose

Sends TCP packets with no flags set.

### Expected Behavior

- Closed Port → RST
- Open Port → No Response

### Why a Penetration Tester Uses It

Useful against some stateless firewalls because no SYN packet is sent.

### Limitations

- Often ineffective against Windows
- Blocked by many stateful firewalls

---

## TCP FIN Scan

```bash
sudo nmap -sF <IP Address>
```

### Purpose

Sends TCP packets with only the FIN flag set.

### Expected Behavior

- Closed Port → RST
- Open Port → No Response

### Why a Penetration Tester Uses It

Alternative scan when SYN scans are not appropriate.

### Limitations

Same limitations as NULL scans.

---

## TCP Xmas Scan

```bash
sudo nmap -sX <IP Address>
```

### Purpose

Sends FIN, PSH, and URG flags simultaneously.

### Expected Behavior

- Closed Port → RST
- Open Port → No Response

### Why a Penetration Tester Uses It

Another alternative TCP flag scan for specific firewall configurations.

### Limitations

Many modern systems and firewalls reduce its effectiveness.

---

## TCP Maimon Scan

```bash
sudo nmap -sM <IP Address>
```

### Purpose

Sends FIN/ACK packets.

### Expected Behavior

Some older systems ignore packets on open ports but return RST packets for closed ports.

### Why a Penetration Tester Uses It

Useful primarily against certain legacy TCP implementations.

### Limitations

Rarely effective on modern operating systems.

---

## TCP Window Scan

```bash
sudo nmap -sW <IP Address>
```

### Purpose

Uses ACK packets and examines the TCP Window Size in returned RST packets.

### Why a Penetration Tester Uses It

Can distinguish open and closed ports on operating systems that implement TCP Window values differently.

### Limitations

Not supported consistently across modern operating systems.

---

## TCP ACK Scan

```bash
sudo nmap -sA <IP Address>
```

### Purpose

Determines whether ports are filtered by a firewall.

### Results

- Filtered
- Unfiltered

### Why a Penetration Tester Uses It

Useful for mapping firewall rules rather than identifying open ports.

### Limitations

Does not determine whether ports are open or closed.

---

## Spoofed Source IP

```bash
sudo nmap -S <Spoofed_IP> <Target_IP>
```

### Purpose

Changes the source IP address inside packets so the target believes another host initiated the scan.

### Networking Concept

Responses are sent to the spoofed IP address rather than the attacker's real IP.

### Why a Penetration Tester Uses It

Used during authorized assessments to evaluate trust relationships or test defensive controls.

### Limitations

The attacker must monitor network traffic to observe responses.

---

## Spoofed MAC Address

```bash
--spoof-mac <MAC_Address>
```

### Purpose

Changes the Layer 2 source MAC address.

### Why a Penetration Tester Uses It

Useful when testing local network security controls.

### Limitations

Only effective on the local network because MAC addresses are not routed.

---

## Decoy Scan

```bash
nmap -D <Decoy_IPs>,ME <Target_IP>
```

### Purpose

Sends scans that appear to originate from multiple IP addresses.

### Why a Penetration Tester Uses It

Makes it more difficult to determine which IP address is performing the scan.

### Limitations

May still be identified by advanced monitoring systems.

---

## Idle (Zombie) Scan

```bash
sudo nmap -sI <Zombie_IP> <Target_IP>
```

### Purpose

Uses a third-party "zombie" host with predictable IP ID values to scan a target indirectly.

### Why a Penetration Tester Uses It

One of the stealthiest scanning techniques because the attacker never communicates directly with the target.

### Limitations

Requires a suitable zombie host with predictable IP ID behavior.

---

# What I Learned

This room taught me that advanced scan types exist because different networks and firewall configurations require different approaches. Understanding the behavior and limitations of each scan is more valuable than simply memorizing commands.

---

# Real-World Application

Advanced Nmap scans allow penetration testers to adapt their reconnaissance strategy depending on the target's firewall configuration, IDS deployment, and operating system behavior. Choosing the correct scan type improves the quality of information gathered while helping the tester understand how the target's defenses respond to different types of traffic.

---

# Interview Notes

## What is the difference between a firewall and an IDS?

A firewall filters traffic according to predefined security rules, while an IDS monitors traffic for suspicious behavior and generates alerts.

---

## Why use advanced scans?

Advanced scans use different TCP flag combinations to gather information in environments where basic scans may not provide useful results due to firewall rules or operating system behavior.

---

## What is IP spoofing?

IP spoofing changes the source IP address in a packet so the target believes another host sent the traffic. Responses are sent to the spoofed IP rather than the attacker's real IP.

---

## Which scan interested you the most?

The Spoofed Source IP scan interested me the most because it demonstrated how attackers can change the source IP field in packets and why monitoring network traffic is necessary to observe responses.

---

# Key Takeaway

Understanding why advanced scans work is more important than memorizing every Nmap command. A penetration tester should understand TCP flags, firewall behavior, IDS detection, and the strengths and limitations of each scan type so they can choose the most appropriate technique for the target environment.

---

# Skills Developed

- Advanced Nmap Scanning
- Firewall Analysis
- IDS Awareness
- TCP Flag Analysis
- TCP NULL Scan
- TCP FIN Scan
- TCP Xmas Scan
- TCP ACK Scan
- TCP Window Scan
- TCP Maimon Scan
- IP Spoofing
- MAC Address Spoofing
- Decoy Scanning
- Idle (Zombie) Scanning
- Network Reconnaissance

---

# Screenshots

This room focused on understanding advanced scanning techniques, TCP flag behavior, firewall interactions, and IDS awareness through Nmap command demonstrations. Screenshots were not necessary because the emphasis was on learning the concepts and scan behavior rather than documenting exploitation or evidence collection.

---

# Personal Reflection

The biggest lesson I learned from this room is that understanding how advanced scans work is more important than memorizing every Nmap command. If I understand the purpose, TCP flags, and limitations of each scan, I can always look up the syntax when needed.

I also learned that different firewall configurations respond differently to various scan types, making it important to understand multiple scanning techniques instead of relying on a single approach.

The Spoofed Source IP scan interested me the most because I had always wondered how IP spoofing worked. Learning that responses are sent to the spoofed IP instead of the attacker's real IP helped me understand the entire process.

This room will help me during future penetration tests because I now understand that advanced scan types provide additional options when basic scans do not produce useful results, allowing me to adapt my reconnaissance strategy to different network environments.