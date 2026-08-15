 # Nmap Post Port Scans

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Nmap Post Port Scans  
**Date Completed:** August 15, 2026  
**Difficulty:** Medium  
**Room Type:** Reading + Nmap Command Demonstrations

---

# Objective

The objective of this room was to learn how to identify services and software versions running on open ports, fingerprint a target's operating system, trace the network path to a target, use the Nmap Scripting Engine (NSE) for additional enumeration, and save scan results for documentation and future analysis.

---

# Why Post Port Scans Matter

Finding an open port is only the beginning of reconnaissance. Post port scans provide additional information such as the service running on the port, its software version, the target's operating system, and other details that help identify potential vulnerabilities and attack vectors.

---

# Networking Concepts

## Service Enumeration

Service enumeration is the process of identifying the services running on open ports and gathering additional information such as software versions and configurations.

Example:

```
22/tcp open ssh
80/tcp open http
```

---

## Version Detection

Version detection identifies the exact software version running on a service.

Example:

```
Apache httpd 2.4.49
```

Knowing the version allows a penetration tester to research:

- Known CVEs
- Public exploits
- Vendor advisories
- Misconfigurations

---

## Operating System Fingerprinting

Operating system fingerprinting analyzes network responses to estimate the operating system running on the target.

Nmap examines characteristics such as:

- TCP responses
- TCP Window Size
- TTL values
- TCP Options

---

## Traceroute

Traceroute maps the network path between the scanning system and the target.

It helps identify:

- Intermediate routers
- Network topology
- Packet filtering
- Connectivity issues

---

## Nmap Scripting Engine (NSE)

The Nmap Scripting Engine allows Nmap to execute scripts that perform additional enumeration and security checks.

Common script categories include:

- Discovery
- Enumeration
- Safe
- Version
- Vulnerability

---

## Saving Scan Results

Saving scan results allows penetration testers to:

- Document findings
- Compare scans over time
- Include evidence in reports
- Share results with team members
- Review findings later

---

# Commands Learned

## Version Detection

```bash
nmap -sV <IP Address>
```

### Purpose

Identifies the services and software versions running on open ports.

### Why a Penetration Tester Uses It

Determining the exact software version allows for vulnerability research and exploit identification.

### Limitations

Version detection may not always identify the exact version if the service hides or modifies its banner.

---

## Operating System Detection

```bash
sudo nmap -O <IP Address>
```

### Purpose

Attempts to identify the operating system running on the target.

### Networking Concepts

Uses TCP/IP fingerprinting by analyzing packet responses.

### Limitations

Accuracy depends on the number of open and closed ports available for fingerprinting.

---

## Traceroute

```bash
nmap --traceroute <IP Address>
```

### Purpose

Maps the path packets take to reach the target.

### Why a Penetration Tester Uses It

Useful for understanding network topology and identifying where traffic may be filtered.

### Limitations

Some routers block or filter traceroute packets.

---

## Nmap Scripting Engine

```bash
nmap --script default <IP Address>
```

### Purpose

Executes predefined Nmap scripts for additional enumeration.

### Why a Penetration Tester Uses It

Automates common reconnaissance tasks such as service enumeration, banner grabbing, and security checks.

### Limitations

Some scripts generate additional traffic and may trigger security monitoring systems.

---

## Saving Scan Results

```bash
nmap -oN scan.txt <IP Address>
```

### Purpose

Saves scan results in normal text format.

### Why a Penetration Tester Uses It

Useful for documentation, reporting, and reviewing findings later.

---

# What I Learned

This room taught me that identifying services, software versions, and operating systems is one of the most important parts of reconnaissance. Knowing exactly what is running on a target allows a penetration tester to research vulnerabilities and plan the next phase of an assessment.

---

# Real-World Application

During a penetration test, service enumeration and version detection provide the information needed to identify potential vulnerabilities. Operating system fingerprinting, traceroute, and NSE scripts help build a more complete understanding of the target environment before exploitation begins.

---

# Interview Notes

## What is service enumeration?

Service enumeration is the process of identifying the services running on open ports and collecting additional information such as software versions and configurations.

---

## Why is version detection important?

Knowing the exact software version allows a penetration tester to research known vulnerabilities, CVEs, and exploits that may affect the target.

---

## What is OS fingerprinting?

OS fingerprinting identifies the target's operating system by analyzing TCP/IP responses and packet characteristics.

---

## What is the Nmap Scripting Engine?

The Nmap Scripting Engine (NSE) is a collection of scripts that extend Nmap's functionality by automating tasks such as service enumeration, vulnerability detection, and security checks.

---

# Key Takeaway

Simply knowing that a port is open is not enough. A penetration tester must identify the service, determine its version, fingerprint the operating system, and gather as much information as possible before researching vulnerabilities and planning exploitation.

---

# Skills Developed

- Service Enumeration
- Version Detection
- Operating System Fingerprinting
- Traceroute
- Nmap Scripting Engine (NSE)
- Banner Grabbing
- Network Mapping
- Reconnaissance
- Nmap Reporting

---

# Screenshots

This room focused on understanding post-port scanning techniques, service enumeration, version detection, operating system fingerprinting, traceroute, and NSE scripts through Nmap command demonstrations. Screenshots were not necessary because the emphasis was on understanding reconnaissance techniques rather than documenting exploitation or evidence collection.

---

# Personal Reflection

The biggest lesson I learned from this room is that identifying the operating system, services, and software versions running on a target provides valuable information for vulnerability research. Once I know exactly what software is running, I can research known CVEs and determine potential attack paths.

I also learned that service enumeration is much more valuable than simply identifying an open port because it reveals what application is running, its version, and how it might be exploited.

Traceroute was the feature that interested me the most because it helped me better understand how packets travel across a network and how network topology can be mapped.

This room will help me during future penetration tests because it taught me how to gather detailed information after discovering open ports, making my reconnaissance more thorough and helping me identify potential vulnerabilities before attempting exploitation.