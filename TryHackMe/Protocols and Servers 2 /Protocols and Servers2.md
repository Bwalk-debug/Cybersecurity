 # Protocols and Servers 2

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Protocols and Servers 2  
**Date Completed:** August 10, 2026  
**Difficulty:** Medium  
**Room Type:** Reading + Command Demonstrations

---

# Objective

The objective of this room was to explain common attacks against network communications, including packet sniffing, Man-in-the-Middle (MITM) attacks, and password attacks. The room also introduced TLS and secure protocols that organizations use to protect sensitive information while it travels across a network.

---

# Key Concepts

## Packet Sniffing

Packet sniffing is the process of capturing and analyzing network traffic as it travels across a network. While network administrators use packet sniffing for troubleshooting, attackers may use it to capture usernames, passwords, cookies, and other sensitive information if the traffic is not encrypted.

---

## Man-in-the-Middle (MITM)

A Man-in-the-Middle attack occurs when an attacker secretly positions themselves between two communicating devices. Both users believe they are communicating directly with one another while the attacker intercepts, monitors, or even modifies the traffic being exchanged.

---

## Password Attacks

The room introduced several common password attacks:

- **Brute Force** – Attempts every possible password combination.
- **Dictionary Attack** – Uses a list of common passwords.
- **Credential Stuffing** – Uses username/password combinations leaked from previous data breaches.
- **Password Guessing** – Makes educated guesses based on information about the target.
- **Password Spraying** – Tries one common password against many user accounts to avoid account lockouts.
- **Hybrid Attack** – Combines dictionary words with numbers, symbols, or variations.

---

# Networking Concepts

## TLS (Transport Layer Security)

TLS is a cryptographic protocol that encrypts data while it travels across a network. It protects the confidentiality and integrity of communications by preventing attackers from reading or modifying intercepted traffic.

---

## HTTP vs HTTPS

### HTTP

- **Protocol:** HTTP
- **Port:** 80/TCP
- **Encryption:** None

HTTP sends all communication in plain text, making it vulnerable to packet sniffing and Man-in-the-Middle attacks.

---

### HTTPS

- **Protocol:** HTTPS
- **Port:** 443/TCP
- **Encryption:** TLS

HTTPS encrypts communication between clients and servers, protecting sensitive information such as usernames, passwords, session cookies, and personal data while it is transmitted.

---

## Secure vs Insecure Protocols

| Insecure Protocol | Secure Alternative |
|-------------------|-------------------|
| HTTP | HTTPS |
| FTP | SFTP / FTPS |
| Telnet | SSH |
| POP3 | POP3S |
| IMAP | IMAPS |
| SMTP | SMTPS / STARTTLS |

---

# Common Network Attacks

## Packet Sniffing

### Goal

Capture network traffic to obtain sensitive information.

### Common Targets

- Usernames
- Passwords
- Cookies
- Email contents
- Files
- Session tokens

### Mitigation

- TLS
- VPNs
- Secure protocols
- Encrypted authentication

---

## Man-in-the-Middle (MITM)

### Goal

Intercept or modify communication between two devices.

### Risks

- Credential theft
- Session hijacking
- Data manipulation
- Information disclosure

### Mitigation

- HTTPS
- TLS
- Certificate validation
- VPNs
- Secure Wi-Fi

---

## Password Attacks

### Goal

Gain unauthorized access by compromising user passwords.

### Mitigation

- Strong password policies
- Multi-Factor Authentication (MFA)
- Account lockout policies
- Password managers
- Monitoring failed login attempts

---

# Commands Learned

## SSH

### Command

```bash
ssh mark@<IP>
```

### Purpose

Establishes an encrypted remote connection to a target system.

### Networking Concepts

- **Protocol:** SSH
- **Port:** 22/TCP
- **Encryption:** Yes
- **Replaces:** Telnet

### Real-World Use

Organizations use SSH to securely administer Linux servers and network devices.

During an authorized penetration test, SSH allows testers to securely access systems after obtaining valid credentials. They can enumerate the system, collect evidence, identify privilege escalation opportunities, and document findings.

---

## SCP (Secure Copy Protocol)

### Command

```bash
scp mark@<IP>:/home/mark/book.txt ~/
```

### Purpose

Securely transfers files between systems using SSH.

### Networking Concepts

- **Protocol:** SCP
- **Port:** 22/TCP
- **Encryption:** Yes

### Real-World Use

Organizations use SCP to securely transfer files between systems.

During an authorized penetration test, SCP can be used to securely copy logs, scripts, reports, or evidence from a target system. In a red team engagement, it may also demonstrate how an attacker could exfiltrate sensitive data if authorized within the engagement scope.

---

# Why This Matters to Penetration Testers

Understanding protocols and secure communications helps penetration testers identify insecure services, determine whether sensitive information is adequately protected, and recommend secure alternatives.

Knowledge of protocols also helps determine:

- Which ports should be open
- Which services are running
- Which encryption methods are being used
- Whether communications are vulnerable to interception

---

# What I Learned

This room taught me that understanding network protocols alone is not enough—it is equally important to understand how they are secured. Encrypting network communications with TLS and replacing insecure protocols with secure alternatives significantly reduces the risk of attackers intercepting sensitive information.

I also learned how common attacks such as packet sniffing, Man-in-the-Middle attacks, and password attacks target network communications and why organizations should implement modern security practices to defend against them.

---

# Real-World Application

During a penetration test, identifying insecure protocols helps determine potential attack vectors and security risks. A penetration tester can verify whether sensitive information is transmitted securely, assess whether organizations are using outdated protocols, and recommend secure alternatives to reduce risk.

---

# Interview Notes

## Why is it important for a penetration tester to understand network protocols?

Understanding network protocols helps penetration testers identify running services, understand how systems communicate, research vulnerabilities, and determine the most effective methods for enumeration and assessment.

---

## Why have protocols like FTP and Telnet been replaced?

Protocols such as FTP and Telnet transmit usernames, passwords, and other sensitive information in plain text. Modern organizations use secure alternatives such as SFTP, SCP, HTTPS, and SSH because they encrypt communications and better protect sensitive data.

---

## Which protocol interested you the most?

The protocol that interested me the most was **IMAP** because it allows users to synchronize and access their email from multiple devices while keeping messages stored on the mail server. Learning how organizations manage email across multiple devices gave me a better understanding of modern email infrastructure.

---

## What is the biggest lesson you learned?

The biggest lesson I learned from this room is that organizations should always use secure protocols whenever possible. Encrypting network communications significantly reduces the risk of attackers intercepting sensitive information during transmission.

---

# Key Takeaway

Understanding how protocols communicate, how they are secured, and how attackers target them is fundamental to penetration testing. Strong networking knowledge allows penetration testers to identify insecure services, recognize attack opportunities, and recommend effective security improvements that protect data in transit.

---

# Skills Developed

- Protocol Security
- TLS
- HTTPS
- SSH
- SCP
- Packet Sniffing
- Man-in-the-Middle Attacks
- Password Attacks
- Network Encryption
- Secure Communications
- Port Identification
- Service Identification
- Networking Fundamentals

---

# Screenshots

This room primarily consisted of networking concepts, protocol security, and command demonstrations. No exploitation or privilege escalation activities were performed.

---

# Personal Reflection

This room reinforced the importance of secure communication in modern networks. Understanding how attackers intercept traffic and how encryption protects sensitive information helped me connect networking concepts with real-world penetration testing. Learning about TLS, secure protocols, and common network attacks strengthened my understanding of how organizations defend their data and how penetration testers evaluate those defenses during an assessment.

I would recommend this room to anyone beginning penetration testing because it builds a strong networking and security foundation. Understanding protocols, encryption, and common attack techniques is essential before moving into more advanced enumeration, exploitation, and web application security.