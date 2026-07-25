 # Cyber Kill Chain

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Cyber Kill Chain  
**Date Completed:** July 25, 2026  
**Difficulty:** Medium

---

# Objective

The objective of this room was to introduce the Cyber Kill Chain framework and explain the seven stages of a cyberattack from an attacker's perspective. The room also demonstrated how defenders can detect, prevent, and respond to attacks at each stage of the kill chain.

---

# What is the Cyber Kill Chain?

The Cyber Kill Chain is a cybersecurity framework developed by Lockheed Martin that describes the stages an attacker follows during a cyberattack. Understanding each phase allows security professionals to identify opportunities to detect, prevent, or disrupt an attack before it reaches its objective.

---

# The Seven Phases of the Cyber Kill Chain

## 1. Reconnaissance

The attacker gathers information about the target organization using public sources, scanning tools, social engineering, or other intelligence-gathering techniques.

---

## 2. Weaponization

The attacker creates or modifies malware or an exploit and prepares it to target the identified vulnerability.

---

## 3. Delivery

The attacker delivers the malicious payload to the victim through methods such as phishing emails, malicious websites, infected USB devices, or compromised downloads.

---

## 4. Exploitation

The delivered payload exploits a vulnerability in the target system to gain initial access.

---

## 5. Installation

After exploitation, malware or another persistence mechanism is installed to maintain access to the compromised system.

---

## 6. Command and Control (C2)

The compromised machine communicates with the attacker's command and control server, allowing the attacker to remotely control the infected system.

---

## 7. Actions on Objectives

The attacker performs their final objective, such as stealing sensitive information, deploying ransomware, disrupting services, or moving laterally throughout the network.

---

# Key Concepts

## Why is Reconnaissance Important?

Reconnaissance is one of the most important phases because every successful attack begins with gathering information. The more information an attacker collects about a target, the easier it becomes to identify vulnerabilities and develop an effective attack plan.

For defenders, limiting publicly available information and reducing the organization's attack surface can make reconnaissance much more difficult.

---

## Attacker vs Defender Perspective

### Attacker

An attacker uses the Cyber Kill Chain as a roadmap to plan and execute a successful attack while minimizing detection.

### Defender

A defender uses the Cyber Kill Chain to identify opportunities to detect, prevent, and interrupt an attack before it reaches its objective.

---

# Defensive Strategies

Organizations can defend against each stage of the Cyber Kill Chain by:

- Limiting publicly available information
- Keeping systems patched and updated
- Deploying endpoint protection
- Using email filtering to prevent phishing attacks
- Monitoring network traffic for suspicious activity
- Detecting Command and Control communications
- Educating employees about cybersecurity awareness
- Implementing the Principle of Least Privilege
- Maintaining strong incident response procedures

---

# What I Learned

The biggest lesson I learned from this room is that becoming a successful penetration tester requires developing the mindset of an attacker. Understanding how attackers think and the steps they follow allows penetration testers to simulate realistic attacks and help organizations strengthen their defenses before malicious attackers can exploit their systems.

I also learned that both attackers and defenders can use the Cyber Kill Chain, but for different purposes. Attackers use it to plan attacks, while defenders use it to detect and stop attacks before significant damage occurs.

---

# Interview Notes

## What is the Cyber Kill Chain?

The Cyber Kill Chain is a cybersecurity framework that describes the seven stages of a cyberattack:

1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control (C2)
7. Actions on Objectives

Security professionals use this framework to better understand how attacks occur and where they can be prevented.

---

## Why should penetration testers understand the Cyber Kill Chain?

Penetration testers should understand the Cyber Kill Chain because it helps them think like an attacker and understand how real-world attacks progress. This allows them to perform realistic security assessments and identify weaknesses before malicious actors can exploit them.

---

## How can defenders use the Cyber Kill Chain?

Defenders can use the Cyber Kill Chain to identify opportunities to detect or stop an attack during each phase. Understanding the framework helps organizations improve monitoring, strengthen security controls, educate employees, and reduce the likelihood of a successful attack.

---

# Key Takeaway

The Cyber Kill Chain provides a structured view of how cyberattacks occur from start to finish. By understanding each phase, penetration testers can perform more realistic security assessments, while defenders can implement controls that interrupt attacks before attackers accomplish their objectives.

---

# Skills Developed

- Cyber Kill Chain Framework
- Attacker Mindset
- Defensive Security Strategies
- Reconnaissance Concepts
- Cybersecurity Methodology
- Security Awareness
- Threat Analysis
- Critical Thinking

---

# Screenshots

This room was concept-based and did not include any hands-on exercises. Therefore, no screenshots were captured.

---

# Personal Reflection

This room reinforced the importance of understanding how attackers think during every stage of an attack. As I continue through the Jr Penetration Tester learning path, I will apply the Cyber Kill Chain framework to better understand how penetration tests simulate real-world attacks and how organizations can improve their defensive security posture.