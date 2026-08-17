 # Content Discovery

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Content Discovery  
**Date Completed:** August 17, 2026  
**Difficulty:** Easy  
**Room Type:** Reading + Hands-on (Gobuster and Web Enumeration)

---

# Objective

The objective of this room was to learn different techniques used to discover hidden content within web applications using manual reconnaissance, OSINT, and automated tools such as Gobuster.

---

# Why Content Discovery Matters

Many web applications contain files, directories, endpoints, and resources that are not linked through the normal user interface. Discovering these hidden resources expands the application's attack surface and may reveal administrative interfaces, sensitive files, or additional functionality that can be further investigated during a penetration test.

---

# Web Application Concepts

## Content Discovery

Content discovery is the process of identifying files, directories, endpoints, and other resources that are not immediately visible to users browsing a web application.

---

## OSINT

Open Source Intelligence (OSINT) is the process of gathering information from publicly available sources.

Examples include:

- Search engines
- GitHub
- robots.txt
- sitemap.xml
- Wayback Machine
- Public documentation
- Social media

OSINT helps penetration testers gather information before directly interacting with the target.

---

## Directory Brute-Forcing

Directory brute-forcing uses wordlists to automatically test common directory and file names against a web server.

The goal is to discover resources that developers forgot to hide or remove.

---

## Gobuster

Gobuster is an enumeration tool that uses wordlists to discover:

- Hidden directories
- Hidden files
- Virtual hosts
- DNS subdomains

It is one of the most commonly used web reconnaissance tools during penetration tests.

---

# HTTP Response Codes

Understanding HTTP response codes is essential during directory enumeration.

## 200 OK

The requested resource exists and is accessible.

---

## 301 Moved Permanently

The resource exists but redirects to another location.

---

## 302 Found

The requested resource temporarily redirects.

---

## 403 Forbidden

The resource exists, but access is denied.

Although access is restricted, this response confirms that the directory or file exists and may warrant additional investigation during an authorized assessment.

---

## 404 Not Found

The requested resource does not exist.

---

# Manual Content Discovery

Manual techniques include:

- Viewing Page Source
- Inspecting JavaScript files
- Checking robots.txt
- Reviewing sitemap.xml
- Searching GitHub
- Using search engines
- Reviewing archived pages

---

# Automated Content Discovery

## Gobuster Directory Enumeration

```bash
gobuster dir -u http://TARGET_IP -w WORDLIST
```

### Purpose

Uses a wordlist to enumerate hidden directories and files on a web server.

### Why a Penetration Tester Uses It

Automates the discovery of hidden resources that may contain sensitive information or vulnerable functionality.

### Limitations

- Depends on the quality of the wordlist.
- May trigger security monitoring or rate limiting.
- Hidden resources may still require authentication.

---

# What I Learned

This room taught me that content discovery is one of the most important phases of web application reconnaissance. Hidden resources often provide valuable information that expands the attack surface and guides further testing.

---

# Real-World Application

During a web application penetration test, content discovery helps identify hidden directories, administrative interfaces, backup files, and other resources that may expose sensitive information or vulnerable functionality. Combining manual reconnaissance with automated tools provides a more complete understanding of the target application.

---

# Interview Notes

## What is content discovery?

Content discovery is the process of identifying hidden files, directories, endpoints, and other resources within a web application that are not directly linked through the user interface.

---

## Why is content discovery important?

It expands the application's attack surface by revealing resources that may contain sensitive information or vulnerabilities.

---

## What is Gobuster?

Gobuster is an enumeration tool that uses wordlists to discover hidden directories, files, virtual hosts, and DNS subdomains.

---

## Why is a 403 Forbidden response valuable?

A 403 response confirms that the requested resource exists even though access is denied. This tells a penetration tester that the directory or file may be worth further investigation during an authorized assessment.

---

# Key Takeaway

Content discovery is much more than finding hidden folders. It helps uncover additional attack surfaces, identify sensitive resources, and build a more complete understanding of a web application before attempting exploitation.

---

# Skills Developed

- Content Discovery
- Web Application Reconnaissance
- Gobuster
- Directory Enumeration
- OSINT
- HTTP Response Codes
- Hidden Resource Discovery
- Attack Surface Identification

---

# Screenshots

This room focused on manual and automated web application reconnaissance using Gobuster and content discovery techniques. Screenshots were optional because the emphasis was on understanding the discovery process and interpreting enumeration results rather than documenting exploitation.

---

# Personal Reflection

The biggest lesson I learned from this room is that content discovery plays a critical role in web application reconnaissance. Discovering hidden directories, files, and endpoints provides additional information that can make a penetration test more effective by revealing attack surfaces that are not immediately visible.

I also learned that content discovery is more valuable than only examining the visible pages because many web applications contain hidden resources that are not linked through the user interface.

Gobuster interested me the most because it automates directory enumeration and helps discover hidden directories that may not be visible through normal browsing.

This room will help me during future web application penetration tests because it taught me how to discover hidden resources that may contain sensitive information or vulnerable functionality before attempting exploitation.