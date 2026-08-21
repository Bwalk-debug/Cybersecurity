 # Web Server Attacks - 1

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Web Server Attacks - 1  
**Date Completed:** August 21, 2026  
**Difficulty:** Medium  
**Room Type:** Mainly Reading + Hands-on Commands

---

# Objective

The objective of this room was to learn how to enumerate web servers, identify server software and versions through HTTP response headers, investigate exposed server-status pages and debug endpoints, discover sensitive files such as `.env` files, and use tools such as curl and Nikto to gather information about a target web server.

---

# Why Web Server Enumeration Matters

A web application depends on underlying web server software to process HTTP requests and return responses.

During a penetration test, identifying the web server, software version, exposed files, status pages, and debugging functionality can provide valuable information about the target.

This information can then be used to perform more focused vulnerability research instead of blindly attempting exploits.

---

# Networking Concepts

## Web Server

A web server is software that receives HTTP or HTTPS requests from clients and returns requested web resources.

Common web servers include:

- Apache
- Nginx
- Microsoft IIS

The basic communication process is:

```text
Browser / Client
      |
      | HTTP Request
      v
Web Server
      |
      | HTTP Response
      v
Browser / Client
```

The browser provides the graphical interface, while the web server processes the requests behind the application.

---

# HTTP and HTTPS

HTTP and HTTPS are application-layer protocols used for communication between web clients and servers.

## HTTP

- Default TCP Port: 80
- Encryption: No

## HTTPS

- Default TCP Port: 443
- Encryption: TLS

Web applications can also run HTTP services on non-standard ports such as:

- 3000
- 8000
- 8080

A penetration tester should not assume what service is running based only on the port number. Each listening service should be enumerated individually.

---

# HTTP Response Headers

HTTP response headers contain metadata sent by a web server in response to a client's request.

Example:

```text
HTTP/1.1 200 OK
Server: Apache/2.4.49
Content-Type: text/html
```

The following header could be particularly valuable:

```text
Server: Apache/2.4.49
```

This reveals:

- Web server software: Apache
- Software version: 2.4.49

A penetration tester could then research whether that specific version has known vulnerabilities or CVEs.

Finding a CVE does not automatically mean the target is vulnerable. The tester must determine whether the vulnerability applies to the target's configuration and environment.

---

# Service and Version Enumeration

Identifying the exact software version allows a penetration tester to move from general reconnaissance to focused vulnerability research.

```text
Identify Web Server
        |
        v
Identify Version
        |
        v
Research Known CVEs
        |
        v
Determine Applicability
        |
        v
Test Within Scope
```

This is more effective than randomly attempting exploits and creating unnecessary network traffic.

---

# Multiple Web Services

A single host can expose multiple web applications or services on different ports.

For example:

```text
Port 80   -> Main Website
Port 3000 -> Possible Web Application
Port 8000 -> Possible Testing Service
Port 8080 -> Possible Alternate Web Service
```

These are only examples. The actual service must be enumerated.

Each port could expose different:

- Software
- Versions
- Applications
- Configurations
- Endpoints
- Vulnerabilities

Because of this, each web service should be investigated individually.

---

# Server-Status Pages

A server-status page can expose information about the current activity and state of a web server.

Depending on the server and its configuration, exposed information may include:

- Requests being processed
- Requested URLs
- Server activity
- Client information
- Uptime
- Operational information

Exposing this information publicly can provide a penetration tester with additional reconnaissance data.

---

# Debug Endpoints

Debug functionality is designed to help developers diagnose problems within an application.

If debug functionality is accidentally exposed in a production environment, it may reveal:

- Error messages
- Stack traces
- Internal file paths
- Environment variables
- Application configuration
- Database information
- Internal application details

Debug functionality should therefore be properly restricted in production environments.

---

# Exposed `.env` Files

Applications commonly use `.env` files to store environment-specific configuration.

Depending on the application, these files may contain:

```text
DB_HOST=...
DB_USERNAME=...
DB_PASSWORD=...
API_KEY=...
SECRET_KEY=...
```

If a `.env` file is accidentally publicly accessible, it can result in serious information disclosure.

Potentially exposed credentials should not automatically be assumed to provide administrator or root access. A penetration tester would need to verify whether the credentials work and determine the privileges associated with the account.

---

# Commands Used

## Retrieve Web Content with curl

```bash
curl -s http://MACHINE_IP:8000/
```

### Breakdown

- `curl` — sends a request to the web server.
- `-s` — enables silent mode.
- `http://` — communicates using HTTP.
- `:8000` — connects to TCP port 8000.
- `/` — requests the root resource.

### Purpose

Retrieves the response body returned by the web application.

### Penetration Testing Use

Can be used to inspect content returned by a web service without relying on a graphical browser.

---

## Retrieve HTTP Headers on Port 80

```bash
curl -SI http://MACHINE_IP:80
```

### Breakdown

- `-S` — displays errors when used with silent mode.
- `-I` — retrieves response headers only.
- `80` — standard HTTP TCP port.

### Purpose

Allows a penetration tester to inspect HTTP response headers.

These headers may reveal server software, versions, content types, redirects, or other useful information.

---

## Retrieve HTTP Headers on Port 3000

```bash
curl -sI http://MACHINE_IP:3000
```

### Purpose

Retrieves HTTP response headers from the service listening on TCP port 3000.

Port 3000 is commonly used by web applications and development services, but the actual service must be identified through enumeration.

---

## Retrieve HTTP Headers on Port 8080

```bash
curl -sI http://MACHINE_IP:8080
```

### Purpose

Retrieves HTTP response headers from the web service listening on TCP port 8080.

Port 8080 is commonly used as an alternate HTTP port.

Again, the port number alone does not identify the application.

---

# How curl Works Across the Network

When running:

```bash
curl -sI http://MACHINE_IP:8080
```

The communication can be simplified as:

```text
Pentester
    |
    | TCP Connection :8080
    v
Web Server
    |
    | HTTP Request
    v
Processes Request
    |
    | HTTP Response + Headers
    v
Pentester
```

This involves multiple concepts:

- **TCP** provides transport.
- **Port 8080** identifies the listening network service.
- **HTTP** defines the application-layer communication.
- **curl** acts as the HTTP client.

---

# Nikto

```bash
nikto -h http://MACHINE_IP:80
```

Nikto is an automated web server security scanner.

The `-h` option specifies the target host.

Nikto can perform checks for:

- Interesting files
- Web server misconfigurations
- Potentially dangerous resources
- Outdated server software
- HTTP security issues
- Exposed information

## curl vs Nikto

```text
curl
 |
 +-- Manually send HTTP requests
 |
 +-- Inspect responses and headers


Nikto
 |
 +-- Automate numerous web-server checks
 |
 +-- Identify potential security issues
```

Nikto can generate significantly more traffic than manually inspecting a few HTTP responses, making scope and authorization important during an assessment.

---

# Limitations

## curl

curl only reveals information that the server returns.

A server may:

- Hide its version
- Modify response headers
- Remove identifying headers
- Require authentication
- Restrict certain endpoints

Therefore, missing information does not necessarily mean the information or functionality does not exist.

## Nikto

Automated scanners can:

- Generate significant traffic
- Trigger IDS/IPS alerts
- Produce false positives
- Miss application-specific vulnerabilities

Automated scanning results should therefore be manually validated.

---

# What I Learned

The biggest lesson I learned from this room was that commands and tools such as curl and Nikto can help enumerate web servers during penetration testing engagements.

I learned that web server configuration can expose valuable information through response headers, status pages, debug functionality, and sensitive files.

Identifying this information allows a penetration tester to perform focused vulnerability research instead of randomly attempting exploits.

---

# Real-World Application

During a web application penetration test, web server enumeration helps build a better understanding of the target's infrastructure.

A penetration tester may discover:

```text
Open Web Port
      |
      v
Web Server
      |
      v
Software / Version
      |
      v
Exposed Files or Endpoints
      |
      v
Potential Vulnerabilities
      |
      v
Focused Security Testing
```

This makes reconnaissance more efficient and helps identify potential attack surfaces before exploitation.

---

# Interview Notes

## What is a web server?

A web server is software that receives HTTP or HTTPS requests from clients and returns web resources such as HTML pages, files, images, or application data.

---

## Why identify a web server's version?

Identifying the exact software version allows a penetration tester to research known CVEs and vulnerabilities that may affect that version instead of randomly attempting exploits.

---

## Why check multiple HTTP ports?

A single host can run multiple web services on different ports. Each service may use different software, versions, configurations, and applications, creating separate attack surfaces.

---

## Why are exposed `.env` files dangerous?

`.env` files may contain sensitive application configuration such as database credentials, API keys, and secret values. If publicly accessible, this information may provide an attacker with additional access.

---

## Why are debug endpoints dangerous?

Debug functionality may reveal internal application information such as stack traces, file paths, environment variables, configuration information, or database details.

---

## What is curl?

curl is a command-line tool used to transfer data using various network protocols. During web enumeration, it can be used as an HTTP client to send requests and inspect server responses.

---

## What is Nikto?

Nikto is an automated web server scanner that checks for common security issues, exposed files, outdated software, and web server misconfigurations.

---

# Key Takeaway

Web server enumeration is an important part of web application penetration testing. Identifying the web server, software version, response headers, exposed status pages, debug functionality, and sensitive files can reveal valuable information that helps a penetration tester perform more focused vulnerability research and testing.

---

# Skills Developed

- Web Server Enumeration
- HTTP Response Analysis
- curl
- Nikto
- HTTP/HTTPS Fundamentals
- TCP Port Enumeration
- Service Version Identification
- Web Server Fingerprinting
- Information Disclosure Identification
- Debug Endpoint Enumeration
- Server-Status Enumeration
- `.env` File Exposure
- Vulnerability Research

---

# Personal Reflection

The biggest lesson I learned from this room is that web server enumeration tools and commands can provide valuable information during a penetration testing engagement.

Identifying the exact web server and version is important because it allows me to research known CVEs that may apply to the target instead of randomly attempting exploits and generating unnecessary traffic.

curl interested me the most because it allows me to directly interact with web servers and inspect HTTP responses. If the server exposes identifying information through its headers, this can reveal useful information such as the server software and version.

This room will help me during future web application penetration tests because it familiarized me with commands and tools used during web server enumeration and taught me how exposed server information can lead to vulnerability discovery.