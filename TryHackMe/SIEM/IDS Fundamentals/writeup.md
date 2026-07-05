# TryHackMe - [IDS Fundamentals]

**Date Completed:** 07/05/2026

---

## Objective

The goal of the room was to understand the different IDS and how they work and get familiar with the tools that use it and its syntax

---

## What I Learned

-  IDS monitors network or host activity 
-  HIDS - Host intrusion detection system are to monitor security threats on Host machines and see activity 
-  (NIDS) Network Intrusion Detection system monitors within the whole network for security threats
-  Signature-based IDS looks for known threats
-  Anomaly-Based IDS looks for unusual threats
- 
- 

---

## Key Concepts

- HIDS
- NIDS
- Signature-Based IDS
- Anomaly-Based IDS
- 
- 

---

## Commands Used
sudo snort -q -l /var/log/snort -r Task.pcap -A alert_fast -c /etc/snort/snort.lua
This command shows the traffic capture on the snort.lua file to investigate any suspicious behavior 
## Tools Used

- snort 
- 
- 

---

## Challenges

What confused me?
What confused me was trying to understand and read the log files I had captured
How did I solve it?
I solved it by thinking back to wireshark and how I read traffic on there.
---

## Real-World Use

Where would this be used in an organization?
An organization would use this to to monitor all the suspicious behavior on their network so they can analyze it and mitigate it. 

---

## Key Takeaway
The biggest takeaway I took from this was IDS helps detect security threats and help organizations 
