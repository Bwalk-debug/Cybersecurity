 # Burp Suite: Repeater

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Burp Suite: Repeater  
**Date Completed:** August 24, 2026  
**Difficulty:** Medium  
**Category:** Web Application Security / HTTP Request Manipulation  
**Room Type:** Reading + Hands-on

---

# Objective

The objective of this room was to learn the advanced capabilities of the Burp Suite framework by focusing on the Burp Suite Repeater module.

The room demonstrated how HTTP requests can be captured, inspected, modified, resent, and analyzed to understand how a web server responds to different client-controlled values.

---

# Why Burp Suite Repeater Matters

Web applications communicate with clients through HTTP or HTTPS requests and responses.

When using a web application normally, the graphical interface controls much of what the user can submit. However, the underlying HTTP request may contain additional headers, parameters, cookies, and other values.

Burp Suite Repeater allows a penetration tester to work directly with these requests.

Instead of repeatedly performing the same action through the browser, a tester can capture a request once, modify individual values, resend it, and analyze how the server responds.

This can help identify vulnerabilities that may not be visible through normal interaction with the application.

---

# Key Concepts

## Burp Proxy

Burp Proxy sits between the browser and web server and allows HTTP/HTTPS traffic to be intercepted and inspected.

During the room, I used Burp Proxy to capture HTTP requests generated while interacting with the target web application.

The basic communication flow is:

```text
Browser
   |
   | HTTP Request
   v
Burp Proxy
   |
   | Forward Request
   v
Web Server
```

A captured request can then be sent to other Burp Suite tools such as Repeater for additional testing.

---

## Burp Proxy vs Burp Repeater

Burp Proxy and Burp Repeater serve different purposes.

```text
Browser
   |
   v
Burp Proxy
   |
   | Capture / Intercept Request
   v
Burp Repeater
   |
   | Inspect
   | Modify
   | Resend
   v
Web Server
   |
   | HTTP Response
   v
Burp Repeater
```

**Burp Proxy** is primarily used to intercept and capture HTTP/HTTPS traffic traveling between the browser and web server.

**Burp Repeater** allows a penetration tester to manually modify and repeatedly resend captured HTTP requests while analyzing the resulting responses.

---

# Burp Suite Repeater

Burp Suite Repeater is a manual HTTP request testing tool.

After capturing an HTTP request, the request can be sent to Repeater where different parts of it can be modified.

The modified request can then be sent directly to the web server.

The server's response can be analyzed to determine whether the modification affected the application's behavior.

The general process is:

```text
Capture HTTP Request
        |
        v
Send to Repeater
        |
        v
Inspect Request
        |
        v
Modify Request
        |
        v
Send Request
        |
        v
Server Processes Request
        |
        v
HTTP Response
        |
        v
Analyze Response
```

This allows a penetration tester to make controlled changes without recreating the request through the browser every time.

---

# Inspector

Burp Inspector provides a structured way to view and modify different parts of HTTP requests and responses.

Inspector can make it easier to identify individual pieces of request data instead of manually examining the entire raw request.

During penetration testing, this can help identify values that may be useful to modify and test.

The important distinction is that Inspector is modifying the **HTTP request**, not the source code of the web application.

---

# HTTP Requests

An HTTP request is a message sent from a client to a web server requesting a resource or asking the server to perform an action.

Example:

```http
GET / HTTP/1.1
Host: MACHINE_IP
FlagAuthorised: False
```

An HTTP request may contain:

- Request method
- Requested path
- Headers
- Parameters
- Cookies
- Request body

Burp Repeater allows these values to be manually inspected and modified.

---

# HTTP Responses

An HTTP response is the message returned by the web server after receiving and processing an HTTP request.

```text
Client
   |
   | HTTP Request
   v
Web Server
   |
   | Processes Request
   v
Client
   ^
   | HTTP Response
```

When using Repeater, analyzing the response allows a penetration tester to determine whether modifications to the request changed the application's behavior.

---

# HTTP Request Methods

During the room, I worked with GET and POST requests.

## GET

GET is commonly used to retrieve information or resources from a web server.

```http
GET /account HTTP/1.1
```

## POST

POST is commonly used to send information to a web application.

```http
POST /login HTTP/1.1
```

The exact behavior of GET and POST depends on how the web application implements the endpoint.

---

# HTTP Request Headers

HTTP request headers provide additional information about the request being sent from the client to the web server.

Example:

```http
GET / HTTP/1.1
Host: MACHINE_IP
FlagAuthorised: False
```

Request headers may contain information relating to:

- Host
- Authentication
- Cookies
- Content type
- Client information
- Application-specific values

During penetration testing, modifying request headers can help determine whether a server improperly trusts information controlled by the client.

---

# Request Parameters

Request parameters are values supplied to a web application through an HTTP request.

For example:

```text
/account?id=5
```

The parameter is:

```text
id
```

and its value is:

```text
5
```

A penetration tester could modify the value:

```text
/account?id=6
```

and resend the request to determine whether the application behaves differently.

Changing a parameter does not automatically mean a vulnerability exists. The resulting response must be analyzed to determine whether the server properly validates the request and enforces authorization.

---

# Networking Concepts

## HTTP

HTTP is an application-layer protocol used for communication between web clients and web servers.

**Default TCP Port:** 80  
**Encryption:** No TLS encryption

During this room, the target web service communicated using HTTP on TCP port 80.

---

## HTTPS

HTTPS uses HTTP over an encrypted TLS connection.

**Default TCP Port:** 443  
**Encryption:** TLS

TLS protects information while it travels between the client and server.

---

## HTTP vs HTTPS

```text
HTTP
 |
 +-- Commonly TCP Port 80
 |
 +-- No TLS encryption


HTTPS
 |
 +-- Commonly TCP Port 443
 |
 +-- Uses TLS encryption
```

A port number alone does not guarantee which application-layer protocol is running. The service should still be properly identified during enumeration.

---

## TCP

HTTP and HTTPS commonly rely on TCP for transport.

TCP provides reliable, connection-oriented communication and helps ensure data arrives correctly and in the proper order.

Before communication over a new TCP connection, TCP normally establishes the connection using the three-way handshake:

```text
Client                         Server

SYN -------------------------->

     <------------------ SYN-ACK

ACK -------------------------->
```

After the connection is established, application-layer data such as HTTP requests and responses can be exchanged.

---

# TCP/IP and OSI Layers

The communication used during this room can be connected to networking layers.

```text
Application Layer
HTTP / HTTPS
Burp Suite
        |
        v
Transport Layer
TCP
        |
        v
Network Layer
IP
        |
        v
Data Link Layer
Ethernet / Wi-Fi
```

Burp Suite primarily allows the penetration tester to interact with application-layer HTTP communication.

TCP provides reliable transport, while IP handles addressing and routing between systems.

---

# How Burp Repeater Works Across the Network

When the Send button is pressed in Burp Repeater, Burp sends the HTTP request to the target web server.

```text
Burp Repeater
      |
      | TCP Connection :80
      v
Target Web Server
      |
      | HTTP Request
      v
Processes Request
      |
      | HTTP Response
      v
Burp Repeater
      |
      v
Analyze Response
```

Several networking concepts are involved:

- **HTTP** defines the web request and response communication.
- **TCP** provides reliable transport.
- **Port 80** identifies the HTTP service used during this lab.
- **IP** provides addressing and routing.
- **Burp Repeater** acts as the HTTP client when sending the modified request.

---

# Hands-On Walkthrough

During the hands-on portion, I generated HTTP traffic by interacting with the target web application while Burp Proxy was running.

Burp Proxy captured the HTTP request generated by my interaction with the application.

I then sent the captured request to Burp Repeater.

Inside Repeater, I could inspect the HTTP request, modify its contents, send the modified request to the target web server, and analyze the resulting HTTP response.

The workflow was:

```text
Interact With Target
        |
        v
Generate HTTP Traffic
        |
        v
Burp Proxy Captures Request
        |
        v
Send Request to Repeater
        |
        v
Inspect HTTP Request
        |
        v
Modify Request
        |
        v
Send Modified Request
        |
        v
Analyze Server Response
```

---

# Modifying the FlagAuthorised Header

One of the hands-on exercises involved modifying an authorization-related HTTP header.

The original request contained:

```http
FlagAuthorised: False
```

Using Burp Repeater, I changed the value to:

```http
FlagAuthorised: True
```

I then resent the modified request to the web server.

The server responded by revealing a flag that I was not originally authorized to view.

```text
Original Request
        |
FlagAuthorised: False
        |
        v
Restricted Response


Modified Request
        |
FlagAuthorised: True
        |
        v
Server Processes Request
        |
        v
Restricted Flag Revealed
```

This demonstrated how manipulating client-controlled HTTP request data can reveal weaknesses in how a web application handles authorization.

---

# Client-Side vs Server-Side Trust

Client-side information originates from or can be controlled by the user's system, such as the browser and HTTP requests it generates.

Server-side processing occurs on the web server or application backend.

A server should not blindly trust client-controlled information when making sensitive authorization decisions.

```text
Client
   |
   | FlagAuthorised: True
   v
Server
   |
   | Trusts Client-Controlled Value
   v
Restricted Information Returned
```

If authorization depends only on a value that the client can manipulate, a user may be able to change that value and access information or functionality they should not have.

Authorization should therefore be properly validated on the server side.

---

# HTTPS vs Authorization

One concept I initially confused was HTTPS encryption and server-side authorization.

HTTPS protects information **while it travels across the network**.

It does not prevent the legitimate client from modifying its own HTTP request before the request is encrypted and transmitted.

```text
User Modifies Request
        |
        v
Burp Repeater
        |
        v
Modified Request
        |
        v
TLS Encrypts Communication
        |
        v
Web Server Receives Modified Request
```

Therefore:

```text
HTTPS
   |
   +-- Protects data in transit


Authorization
   |
   +-- Determines what the user is allowed to access
```

Encryption and authorization solve different security problems.

---

# Limitations of Burp Repeater

Burp Repeater is primarily a manual testing tool.

This gives the penetration tester precise control over individual requests but can become inefficient when testing large numbers of values.

```text
Modify Value
     |
     v
Send Request
     |
     v
Analyze Response
     |
     v
Modify Again
     |
     v
Repeat
```

Repeater is useful for careful manual testing but would become slow if thousands of different inputs needed to be evaluated.

---

# What I Learned

The biggest lesson I learned from this room was that HTTP requests can be captured and modified before being resent to a web server.

By changing request data, I can observe whether the web server returns a different response.

I also learned that a web application's normal interface does not necessarily show everything being communicated between the client and server.

Examining and modifying the underlying HTTP requests can help reveal security issues that may not be visible through normal interaction with the application.

---

# Real-World Application

During an authorized web application penetration test, Burp Repeater can be used to manually investigate how an application handles different HTTP request values.

```text
Interact With Application
        |
        v
Capture Request
        |
        v
Inspect Request
        |
        v
Identify Interesting Input
        |
        v
Modify Input
        |
        v
Resend Request
        |
        v
Analyze Response
        |
        v
Potential Vulnerability
        |
        v
Manual Validation
```

Being able to manually manipulate HTTP requests can help identify vulnerabilities that may not be obvious when interacting with the application's normal interface.

---

# Interview Notes

## What is Burp Suite Repeater?

Burp Suite Repeater is a manual testing tool that allows a penetration tester to modify and repeatedly resend HTTP requests to a web server while analyzing the resulting responses.

---

## What is the difference between Burp Proxy and Burp Repeater?

Burp Proxy intercepts and captures HTTP/HTTPS traffic traveling between the browser and web server.

Burp Repeater allows captured HTTP requests to be manually modified, resent, and analyzed.

---

## Why is Burp Repeater useful during a penetration test?

Repeater allows a penetration tester to change individual pieces of an HTTP request and determine how those modifications affect the web server's response.

This can help identify vulnerabilities that may not be visible through normal interaction with the application.

---

## What is an HTTP request?

An HTTP request is a message sent from a client to a web server requesting a resource or asking the server to perform an action.

---

## What is an HTTP response?

An HTTP response is the message returned by a web server after receiving and processing an HTTP request.

---

## What is an HTTP request header?

An HTTP request header provides additional information about a request being sent from the client to the server.

Headers can contain host information, cookies, authentication information, content information, and application-specific values.

---

## What is the difference between HTTP and HTTPS?

HTTP does not provide TLS encryption, while HTTPS uses TLS to encrypt communication between the client and web server.

HTTP commonly uses TCP port 80, while HTTPS commonly uses TCP port 443.

---

## Does HTTPS prevent a user from modifying their own HTTP request?

No.

HTTPS protects the request while it travels across the network, but the client can still modify its own request before the information is encrypted and sent to the server.

---

## Why shouldn't a server trust client-controlled authorization values?

Client-controlled information can potentially be manipulated.

Sensitive authorization decisions should therefore be securely validated by the server instead of relying only on values supplied by the client.

---

## What is a limitation of Burp Repeater?

Burp Repeater is primarily a manual testing tool.

It provides precise control over individual requests but can become inefficient when testing a very large number of different values or payloads.

---

## Which Burp Suite feature interested you the most?

Burp Repeater interested me the most because I was surprised that modifying an HTTP request could cause the web server to respond differently and potentially reveal a vulnerability.

---

# Key Takeaway

The most important lesson from this room was that understanding and manipulating the HTTP communication underneath a web application can reveal security issues that are not immediately visible through the application's graphical interface.

Burp Proxy can capture the communication, while Burp Repeater allows a penetration tester to inspect, modify, resend, and analyze individual HTTP requests.

Understanding how requests, responses, headers, parameters, HTTP/HTTPS, TCP, and server-side authorization work together is more important than simply memorizing where the buttons are inside Burp Suite.

---

# Skills Developed

- Burp Suite
- Burp Proxy
- Burp Repeater
- Burp Inspector
- HTTP Request Analysis
- HTTP Response Analysis
- HTTP Headers
- Request Parameters
- GET Requests
- POST Requests
- HTTP Fundamentals
- HTTPS Fundamentals
- TCP Fundamentals
- TCP Ports 80 and 443
- Client-Server Communication
- Request Manipulation
- Response Analysis
- Client-Side vs Server-Side Trust
- Authorization Testing
- Manual Web Application Testing
- Web Application Penetration Testing

---

# Screenshots

Useful screenshots from this room could include:

- HTTP traffic captured by Burp Proxy
- A captured request sent to Repeater
- The original `FlagAuthorised: False` header
- The modified `FlagAuthorised: True` header
- The resulting HTTP response

Flags or sensitive lab answers should be redacted before screenshots are uploaded to a public GitHub repository.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was that HTTP requests can be captured and modified before being resent to a web server. By changing request data, I can observe whether the server returns a different response.

---

## Why Modifying HTTP Requests Is Important

Being able to modify HTTP requests is important during a web application penetration test because manipulating request data can help identify vulnerabilities that may not be visible when interacting with the application normally through the browser.

---

## Most Interesting Feature

Burp Repeater interested me the most because I was surprised that modifying an HTTP request could cause the web server to return a different response and potentially reveal a vulnerability.

Seeing how the response changed after modifying the request helped me understand why Repeater is useful during web application penetration testing.

---

## Future Penetration Tests

This room will help me during future web application penetration tests because I now understand how modifying HTTP requests and analyzing the server's responses can help identify weaknesses in a web application during authorized testing.