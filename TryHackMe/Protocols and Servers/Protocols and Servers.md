 # Protocols and Servers

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Protocols and Servers  
**Date Completed:** August 9, 2026  
**Difficulty:** Easy  
**Room Type:** Reading + Command Demonstrations

---

# Objective

The objective of this room was to introduce common network protocols and the services that use them, explain how they function, identify their default ports, and discuss the security weaknesses that penetration testers should be aware of during a security assessment.

---

# What is a Network Protocol?

A network protocol is a standardized set of rules that allows devices to communicate across a network. Protocols define how data is transmitted, received, and interpreted between systems.

Without protocols, computers would not know how to communicate with one another.

---

# Protocol vs. Service

A **protocol** defines the rules for communication between devices.

A **service** is the software running on a system that uses a protocol to provide a specific function, such as hosting a website, transferring files, or sending email.

### Example

- **Protocol:** HTTP
- **Service:** Apache or Nginx

Another example:

- **Protocol:** SSH
- **Service:** OpenSSH

Understanding the difference is important because penetration testers communicate using protocols while assessing the services running on target systems.

---

# Why Understanding Protocols is Important

Understanding network protocols helps penetration testers identify running services, understand how systems communicate, research vulnerabilities associated with specific services, and determine the best techniques for enumeration and exploitation.

Protocols also help identify possible attack surfaces during a penetration test.

---

# Protocols Covered

- FTP
- SMTP
- POP3
- IMAP
- Telnet

---

# Networking Concepts

| Protocol | Port | TCP/UDP | Purpose | Secure Alternative |
|----------|------|---------|---------|-------------------|
| FTP | 21 | TCP | File Transfer | SFTP / FTPS |
| SMTP | 25 | TCP | Send Email | SMTPS / STARTTLS |
| POP3 | 110 | TCP | Receive Email | POP3S |
| IMAP | 143 | TCP | Manage Email | IMAPS |
| Telnet | 23 | TCP | Remote Administration | SSH |

---

# Protocol Breakdown

## FTP (File Transfer Protocol)

### Purpose

Transfers files between computers over a network.

### Why Organizations Use It

Organizations use FTP to upload, download, and transfer files between servers and workstations.

### Why FTP is Insecure

FTP transmits usernames, passwords, and files in plain text. Anyone intercepting the traffic can read the information.

### What a Penetration Tester Looks For

- Anonymous login
- Weak credentials
- Sensitive files
- Misconfigured permissions
- Clear-text authentication

---

## SMTP (Simple Mail Transfer Protocol)

### Purpose

Used to send emails between mail clients and mail servers.

### Why Organizations Use It

SMTP is one of the primary protocols used for business communication.

### Why SMTP Can Be Insecure

Without encryption, email contents and authentication information may be transmitted in plain text.

### What a Penetration Tester Looks For

- Open mail relay
- User enumeration
- Weak authentication
- Misconfigured mail servers
- Sensitive email information

---

## POP3 (Post Office Protocol Version 3)

### Purpose

Retrieves emails from a mail server.

### Why Organizations Use It

POP3 allows users to download emails to a local device.

### Why POP3 Can Be Insecure

Standard POP3 sends usernames, passwords, and email contents without encryption.

### What a Penetration Tester Looks For

- Clear-text credentials
- Weak passwords
- Sensitive email contents
- Misconfigured mail services

---

## IMAP (Internet Message Access Protocol)

### Purpose

Allows users to access and manage email while keeping messages stored on the mail server.

### Why Organizations Use It

IMAP allows users to synchronize their email across multiple devices.

### Why IMAP Can Be Insecure

Without encryption, usernames, passwords, and email contents may be transmitted in plain text.

### What a Penetration Tester Looks For

- Weak authentication
- Sensitive emails
- Clear-text credentials
- Misconfigured mail services

---

## Telnet

### Purpose

Provides remote command-line access to another system.

### Why Organizations Used It

Historically, Telnet was used for remote administration of servers and network devices.

### Why Telnet is Insecure

Telnet sends all communication, including usernames, passwords, and commands, in plain text.

### What a Penetration Tester Looks For

- Systems still using Telnet
- Clear-text credentials
- Weak authentication
- Opportunities to demonstrate the risks of unencrypted remote administration

---

# Common Security Risks

Throughout this room, a common security issue appeared across multiple protocols:

- Plain-text authentication
- Plain-text data transmission
- Weak authentication
- Sensitive information exposure

Modern organizations should replace these protocols with secure alternatives whenever possible.

---

# What I Learned

This room taught me that understanding how network protocols work is just as important as understanding how to exploit vulnerabilities. Knowing which protocol a service uses helps identify possible attack surfaces, understand how systems communicate, and determine the appropriate enumeration techniques.

I also learned that many older protocols are insecure because they transmit sensitive information in plain text, making them vulnerable to interception.

---

# Real-World Application

During a penetration test, identifying the protocol and service running on a target system helps determine the next steps in the assessment. Once the service is identified, a penetration tester can research vulnerabilities, enumerate the service, identify misconfigurations, and recommend secure alternatives when necessary.

---

# Interview Notes

## What is a network protocol?

A network protocol is a standardized set of rules that allows devices to communicate across a network by defining how information is transmitted and received.

---

## Why is understanding network protocols important?

Understanding protocols helps penetration testers identify running services, research vulnerabilities, understand communication methods, and determine the best approach for enumeration and testing.

---

## Why have protocols like FTP and Telnet been replaced?

Protocols such as FTP and Telnet have largely been replaced because they transmit usernames, passwords, and other sensitive information in plain text. Modern organizations use secure alternatives such as SFTP, FTPS, and SSH because they encrypt communications.

---

## Which protocol interested you the most?

The protocol that interested me the most was **IMAP** because it allows users to synchronize and access their email from multiple devices while keeping messages stored on the mail server. Learning how organizations manage email across multiple devices gave me a better understanding of modern email infrastructure.

---

# Key Takeaway

Understanding network protocols allows penetration testers to recognize services, identify attack surfaces, understand how systems communicate, and assess security risks associated with each protocol. Strong networking knowledge provides the foundation for effective reconnaissance, enumeration, and vulnerability assessment.

---

# Skills Developed

- Network Protocol Fundamentals
- Service Identification
- Protocol Security
- FTP
- SMTP
- POP3
- IMAP
- Telnet
- Port Identification
- TCP Networking
- Secure Communication Concepts

---

# Screenshots

This room consisted primarily of learning networking concepts and protocol demonstrations. No exploitation or privilege escalation activities were performed.

---

# Personal Reflection

This room reinforced how important networking knowledge is for penetration testing. Learning how protocols work, what services use them, and why some are insecure helps me better understand what I am seeing during reconnaissance and enumeration. It also showed me why modern organizations replace insecure protocols with encrypted alternatives to better protect sensitive information.

I would recommend this room to anyone beginning penetration testing because understanding protocols, ports, and services provides a strong networking foundation that will make future enumeration and exploitation techniques much easier to understand.