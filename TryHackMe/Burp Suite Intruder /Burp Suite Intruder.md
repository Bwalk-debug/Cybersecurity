 # Burp Suite: Intruder

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Burp Suite: Intruder  
**Date Completed:** August 25, 2026  
**Difficulty:** Medium  
**Category:** Web Application Security / Automated HTTP Request Testing  
**Room Type:** Mixed — Reading + Hands-on

---

# Objective

The objective of this room was to learn how Burp Suite Intruder can automate HTTP request manipulation by inserting different payloads into selected positions.

The room demonstrated how Intruder can be used during authorized web application penetration testing for techniques such as fuzzing, credential testing, brute-force testing, and manipulating request values to identify potential vulnerabilities.

---

# Why Burp Suite Intruder Matters

Manually modifying HTTP requests can be useful when investigating a specific request, but performing the same modification hundreds or thousands of times would become repetitive and inefficient.

Burp Suite Intruder helps automate this process.

A penetration tester can select specific parts of an HTTP request, configure payload values, and allow Intruder to automatically send modified requests to the target application.

The responses can then be compared to identify unusual behavior that may require further investigation.

The general workflow is:

```text
Capture HTTP Request
        |
        v
Send to Intruder
        |
        v
Choose Payload Position(s)
        |
        v
Configure Payloads
        |
        v
Choose Attack Type
        |
        v
Start Automated Testing
        |
        v
Multiple HTTP Requests
        |
        v
Multiple HTTP Responses
        |
        v
Compare Results
        |
        v
Investigate Interesting Responses
```

---

# Key Concepts

## Burp Suite Intruder

Burp Suite Intruder is a module within Burp Suite that automates the process of sending modified HTTP requests.

A captured HTTP request can be sent to Intruder where specific values are selected as payload positions.

Intruder then automatically replaces those values with configured payloads and sends the resulting requests to the web server.

The responses can then be analyzed to identify differences or unexpected behavior.

---

# Burp Proxy vs Repeater vs Intruder

The Burp Suite tools I have learned so far serve different purposes.

```text
Burp Proxy
     |
     +-- Capture / Intercept HTTP Requests
     |
     v
Captured Request
     |
     +----------------------+
     |                      |
     v                      v
Repeater                 Intruder
     |                      |
Manual Testing          Automated Testing
     |                      |
Modify Request          Configure Payloads
     |                      |
Resend                  Send Many Requests
     |                      |
Analyze Response        Compare Responses
```

**Burp Proxy** captures and intercepts HTTP/HTTPS traffic.

**Burp Repeater** allows individual HTTP requests to be manually modified and resent.

**Burp Intruder** automates request modification by inserting different payload values into selected positions and sending multiple requests.

---

# Payloads

A payload in Burp Intruder is a value that Intruder inserts into a selected part of an HTTP request.

A payload is not automatically an exploit.

Depending on what is being tested, payloads could contain:

- Usernames
- Passwords
- Numbers
- Strings
- Ticket IDs
- Test inputs
- Other application-specific values

For example:

```text
password=§PAYLOAD§
```

Intruder could automatically test:

```text
password=password1
password=example123
password=summer2026
password=test123
```

Each value becomes a different request.

---

# Payload Positions

A payload position tells Burp Intruder which part of the HTTP request should be replaced with payload values.

Intruder represents selected payload positions using markers similar to:

```text
§value§
```

For example:

```text
username=admin&password=§password§
```

Intruder knows that the password value should change while the rest of the request remains structured according to the configured attack.

The basic process is:

```text
Captured HTTP Request
        |
        v
Select Value to Test
        |
        v
Mark Payload Position
        |
        v
Configure Payload List
        |
        v
Intruder Replaces Value
```

---

# Fuzzing

Fuzzing involves sending many different or unexpected inputs to an application and observing how the application responds.

The goal is to identify behavior such as:

- Errors
- Unexpected responses
- Hidden functionality
- Input-handling problems
- Potential vulnerabilities

Intruder helps automate this process by inserting payloads into selected request positions and sending the modified requests automatically.

---

# Brute-Force Testing

Brute-force testing involves systematically trying multiple possible values until a valid value is identified.

For authentication testing, this may involve testing multiple password candidates against an account during an authorized security assessment.

Instead of manually entering every password candidate, Intruder can automate the requests.

```text
Known Username
      |
      +-- Password 1
      |
      +-- Password 2
      |
      +-- Password 3
      |
      +-- Password 4
      |
      v
Analyze Responses
```

The password guesses are not necessarily random. They may come from a configured wordlist or another generated set of candidate values.

---

# Credential Stuffing

Credential stuffing involves testing known username and password combinations against another authentication system to determine whether credentials have been reused.

Conceptually:

```text
Username1 : Password1
Username2 : Password2
Username3 : Password3
Username4 : Password4
```

This differs from traditional password brute forcing.

```text
Brute Force

Known Username
      |
      +-- Password1
      +-- Password2
      +-- Password3
      +-- Password4
```

Credential stuffing instead uses username/password pairs that already correspond with each other.

---

# Intruder Attack Types

Burp Intruder provides different attack types that control how payloads are inserted into selected positions.

Understanding how each attack type works is important because different testing situations require different payload behavior.

---

## Sniper

Sniper systematically tests payload values against selected payload positions.

Conceptually:

```text
Payload List

A
B
C
D

        ↓

Selected Position

password=§VALUE§
```

Intruder substitutes the payload values into the selected position.

```text
password=A
password=B
password=C
password=D
```

### Why a Penetration Tester Uses It

Sniper is useful when focused testing is needed against particular request values.

### Limitation

Testing large payload lists can generate significant numbers of HTTP requests and requires the resulting responses to be analyzed.

---

## Battering Ram

Battering Ram uses the same payload value across multiple selected payload positions within each request.

For example:

```text
Payload = test
```

could produce:

```text
username=test&password=test
```

The next payload:

```text
Payload = admin
```

could produce:

```text
username=admin&password=admin
```

### Why a Penetration Tester Uses It

Battering Ram is useful when the same test value needs to appear in multiple locations within the request.

### Limitation

It is not appropriate when each payload position requires independent or differently paired values.

---

## Pitchfork

Pitchfork uses multiple payload sets and advances them together.

For example:

```text
Payload Set 1       Payload Set 2

user1          +    password1
user2          +    password2
user3          +    password3
```

Intruder would test:

```text
user1 : password1
user2 : password2
user3 : password3
```

### Why a Penetration Tester Uses It

Pitchfork is useful when values from different payload lists are intended to correspond with each other.

### Limitation

Pitchfork does not test every possible combination between the payload sets.

---

## Cluster Bomb

Cluster Bomb uses multiple payload sets and tests combinations between them.

For example:

```text
Users

admin
user


Passwords

pass1
pass2
pass3
```

The resulting combinations would include:

```text
admin : pass1
admin : pass2
admin : pass3

user  : pass1
user  : pass2
user  : pass3
```

The easiest way to remember the difference between Pitchfork and Cluster Bomb is:

```text
Pitchfork

A1 + B1
A2 + B2
A3 + B3


Cluster Bomb

Every A × Every B
```

### Why a Penetration Tester Uses It

Cluster Bomb is useful when multiple values need to be tested in different combinations.

### Limitation

The number of requests can increase quickly as the number and size of payload sets increase.

---

# Macros

During the hands-on portion, I used a Burp Suite macro as part of an administrator authentication exercise.

The macro automated a request process involving a login token.

Some web applications use values that change between requests, such as anti-CSRF tokens or other session-related values.

Conceptually:

```text
Obtain Required Token
        |
        v
Insert Token Into Request
        |
        v
Send Authentication Request
        |
        v
New Token Required
        |
        v
Repeat
```

A macro can automate the required request sequence instead of requiring the penetration tester to manually obtain and update the token for every request.

---

# Networking Concepts

## HTTP

HTTP is an application-layer protocol used for communication between web clients and web servers.

**Default TCP Port:** 80  
**Encryption:** No TLS encryption

Burp Intruder manipulates application-layer HTTP request data before sending requests to the target web application.

---

## HTTPS

HTTPS uses HTTP over an encrypted TLS connection.

**Default TCP Port:** 443  
**Encryption:** TLS

HTTPS protects communication while it travels across the network.

A penetration tester using Burp can still modify their own authorized requests before those requests are encrypted and transmitted.

---

## TCP

HTTP and HTTPS commonly use TCP as their transport protocol.

TCP provides reliable, connection-oriented communication between systems.

The basic TCP connection begins with the three-way handshake:

```text
Client                         Server

SYN -------------------------->

     <------------------ SYN-ACK

ACK -------------------------->
```

Application-layer HTTP requests and responses can then be exchanged over the connection.

---

# TCP/IP and OSI Layers

Burp Intruder primarily operates with application-layer HTTP/HTTPS communication.

```text
Application Layer
HTTP / HTTPS
Burp Suite Intruder
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

Intruder modifies the HTTP request data, while TCP and IP handle the underlying network communication.

---

# How Intruder Works Across the Network

Burp Intruder can generate significantly more network traffic than manually testing individual requests with Repeater.

For each payload, Intruder can generate another HTTP request.

```text
Burp Intruder
      |
      | Request + Payload 1
      v
Web Server
      |
      | Response 1
      v
Burp Intruder


Burp Intruder
      |
      | Request + Payload 2
      v
Web Server
      |
      | Response 2
      v
Burp Intruder


Burp Intruder
      |
      | Request + Payload 3
      v
Web Server
      |
      | Response 3
      v
Burp Intruder
```

This process continues according to the configured payloads and attack type.

Because automated testing can generate large numbers of requests, it is important that this activity remains within the authorized scope and testing conditions of a penetration test.

---

# Analyzing Intruder Results

Sending payloads is only part of using Intruder.

The resulting HTTP responses must also be analyzed.

During the room, I looked at:

- HTTP response status codes
- Response length
- Differences between responses

An unusual response can indicate that a particular payload caused the application to behave differently.

Common HTTP status-code categories include:

```text
2xx → Successful HTTP request
3xx → Redirection
4xx → Client-side request error
5xx → Server-side error
```

However, a status code alone does not determine whether a payload was successful.

For example, both a successful and failed login could potentially return:

```text
200 OK
```

while containing different response content or response lengths.

Therefore, interesting responses should be investigated further rather than assuming a particular status code proves that a vulnerability exists.

---

# Rate Limiting

Rate limiting restricts how frequently requests can be made to an application.

Without appropriate rate limiting or other authentication protections, an attacker may be able to make large numbers of authentication attempts in a short period of time.

Conceptually:

```text
Repeated Login Attempts
        |
        v
Rate-Limit Threshold
        |
        v
Requests Slowed / Blocked / Challenged
```

Rate limiting does not prevent a user from modifying their own HTTP request.

Instead, it helps reduce the effectiveness of excessive automated requests, including automated password-guessing attempts.

---

# Hands-On Walkthrough

During the hands-on portion, I used Burp Intruder to automate modifications to captured HTTP requests.

The general workflow was:

```text
Interact With Web Application
        |
        v
Capture Request With Burp Proxy
        |
        v
Send Request to Intruder
        |
        v
Choose Payload Position
        |
        v
Configure Payloads
        |
        v
Select Attack Type
        |
        v
Start Automated Requests
        |
        v
Analyze Responses
```

---

# Login Credential Testing

During one authentication exercise, I used the Sniper attack type while testing login-related request data.

Intruder allowed me to automate the process of inserting payload values into the selected position instead of manually changing and resending the request for every test.

This demonstrated how Intruder can reduce repetitive manual work during authorized authentication testing.

---

# Support Ticket Testing

During another hands-on exercise, I used Intruder while testing support-ticket-related request values.

I modified ticket-related values through automated payloads and analyzed the resulting responses.

By investigating different ticket numbers, I was able to locate the response containing the required lab flag.

This demonstrated how automated request manipulation can help identify differences in application behavior that deserve further investigation.

---

# Administrator Authentication and Macro

During the final hands-on portion, I used Intruder again while testing administrator authentication.

This exercise also required creating a macro to automate a process involving the login token.

The macro allowed the required token-related request process to occur automatically while Intruder performed the testing.

This demonstrated that automated web testing sometimes requires more than simply replacing a request value because applications may depend on changing tokens, sessions, or request sequences.

---

# Intruder vs Repeater

Burp Intruder and Burp Repeater can complement each other during a penetration test.

```text
Intruder
   |
   v
Automate Many Tests
   |
   v
Compare Responses
   |
   v
Identify Interesting Result
   |
   v
Repeater
   |
   v
Manually Reproduce Request
   |
   v
Investigate Behavior
   |
   v
Validate Potential Vulnerability
```

Intruder helps identify interesting behavior efficiently.

Repeater can then be used for more controlled manual investigation.

A different response does not automatically prove that a vulnerability exists.

---

# Limitations of Burp Intruder

Burp Intruder provides useful automation, but it also has limitations.

Automated testing can:

- Generate significant network traffic
- Produce large numbers of responses
- Trigger rate limiting
- Trigger security monitoring
- Require manual analysis of interesting results
- Require additional handling for changing tokens or sessions
- Potentially affect application performance if testing is too aggressive

Most importantly, Intruder does not automatically determine whether an unusual response represents a real vulnerability.

Interesting behavior must still be understood and validated.

---

# What I Learned

The biggest lesson I learned from this room was that different payloads and Intruder attack types can be used depending on the values I want to test and the results I am trying to obtain.

Understanding what part of the HTTP request I am testing helps me choose the appropriate payloads and attack type for the situation.

I also learned how automated request testing can save time compared with repeatedly modifying requests manually.

---

# Real-World Application

During an authorized web application penetration test, Burp Intruder can automate repetitive HTTP request testing.

A penetration tester can:

```text
Capture HTTP Request
        |
        v
Identify Value to Test
        |
        v
Select Payload Position
        |
        v
Choose Payloads
        |
        v
Choose Appropriate Attack Type
        |
        v
Automate Requests
        |
        v
Compare Responses
        |
        v
Identify Interesting Behavior
        |
        v
Manually Validate Results
```

Choosing the correct payload configuration depends on what the penetration tester is trying to test.

Automation can save significant time, but the results still require human analysis.

---

# Interview Notes

## What is Burp Suite Intruder?

Burp Suite Intruder is a tool that automates HTTP request testing by inserting configured payloads into selected positions within a request and sending multiple modified requests to a web application.

---

## What is a payload?

A payload is a value that Burp Intruder inserts into a selected payload position.

Payloads can contain usernames, passwords, numbers, strings, IDs, or other test values depending on what is being tested.

---

## What is a payload position?

A payload position identifies the part of an HTTP request that Intruder should replace with payload values during automated testing.

---

## What is the difference between Repeater and Intruder?

Repeater is primarily used for controlled manual request modification and testing.

Intruder automates the process of inserting payloads and sending multiple modified requests.

---

## What is fuzzing?

Fuzzing involves sending different or unexpected inputs to an application and analyzing its behavior for errors, unusual responses, or potential vulnerabilities.

---

## What is the difference between brute forcing and credential stuffing?

Password brute forcing systematically tests multiple password candidates.

Credential stuffing tests known username and password pairs to determine whether credentials have been reused.

---

## What is Sniper?

Sniper systematically tests payload values against selected positions and is useful for focused testing of particular request values.

---

## What is Battering Ram?

Battering Ram inserts the same payload value into multiple selected positions within a request.

---

## What is Pitchfork?

Pitchfork uses multiple payload sets and advances the values together.

For example:

```text
A1 + B1
A2 + B2
A3 + B3
```

---

## What is Cluster Bomb?

Cluster Bomb tests combinations between multiple payload sets.

For example:

```text
Every A × Every B
```

---

## What is the difference between Pitchfork and Cluster Bomb?

Pitchfork pairs corresponding values from multiple payload sets.

Cluster Bomb tests combinations between the payload sets.

---

## What is a Burp macro?

A macro automates a sequence of HTTP requests.

During this room, I used a macro to automate a process involving the login token required for the administrator authentication exercise.

---

## How can you identify interesting Intruder responses?

Response status codes, response lengths, and response content can be compared to identify outliers.

A different response should then be investigated to determine why the application behaved differently.

---

## Why is rate limiting important?

Rate limiting helps prevent excessive automated requests by restricting how frequently requests can be made.

This can reduce the effectiveness of automated password-guessing attacks.

---

## What is a limitation of Intruder?

Intruder can generate large amounts of network traffic and many responses that require analysis.

An unusual response also does not automatically mean that a vulnerability exists, so results should be manually investigated and validated.

---

## Which Intruder attack type interested you the most?

Sniper interested me the most because it was direct and straightforward. It allowed me to select the part of the HTTP request I wanted to test and systematically send different payload values against that position.

---

# Key Takeaway

Burp Suite Intruder extends the HTTP request manipulation concepts learned with Repeater by introducing automation.

Instead of manually modifying and resending every request, Intruder can automatically insert payloads into selected request positions and send multiple requests.

The important skill is not simply knowing how to start Intruder.

A penetration tester should understand:

```text
What am I testing?
        ↓
Which request value matters?
        ↓
Where should the payload go?
        ↓
Which payloads make sense?
        ↓
Which attack type fits the situation?
        ↓
What changed in the responses?
        ↓
Does the result require further investigation?
```

Understanding those decisions is more important than memorizing the interface.

---

# Skills Developed

- Burp Suite
- Burp Proxy
- Burp Intruder
- Burp Repeater
- HTTP Request Analysis
- HTTP Response Analysis
- Automated Request Testing
- Payload Configuration
- Payload Positions
- Sniper Attacks
- Battering Ram Attacks
- Pitchfork Attacks
- Cluster Bomb Attacks
- Fuzzing Fundamentals
- Brute-Force Testing Concepts
- Credential Stuffing Concepts
- HTTP Status Code Analysis
- Response Length Analysis
- Rate Limiting Awareness
- Burp Macros
- Token Handling
- Authentication Testing
- Manual Result Validation
- Web Application Penetration Testing

---

# Screenshots

Useful screenshots from the hands-on portion could include:

- HTTP request captured through Burp Proxy
- Request configured inside Intruder
- Selected payload positions
- Sniper attack configuration
- Pitchfork attack configuration
- Payload configuration
- Intruder results showing different response lengths or status codes
- Support-ticket testing
- Macro configuration
- Administrator authentication testing

Flags, credentials, tokens, or other sensitive lab answers should be redacted before screenshots are uploaded to a public GitHub repository.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was that different payloads and Intruder attack types can be used depending on the values I want to test and the results I am trying to obtain.

Understanding what part of the HTTP request I am testing helps me choose the appropriate payloads and attack type for the situation.

---

## Why Automated Request Testing Is Important

Automated request testing is important during a web application penetration test because it saves time and reduces repetitive manual work.

Instead of modifying and resending every HTTP request individually, Burp Intruder can automatically test multiple payloads while allowing the penetration tester to analyze the resulting responses.

---

## Most Interesting Feature

The Sniper attack type interested me the most because it was direct and straightforward.

It allowed me to select the part of the HTTP request I wanted to test and systematically send different payload values against the selected position.

---

## Future Penetration Tests

This room will help me during future web application penetration tests because it gave me hands-on experience with Burp Intruder and taught me how different payloads and attack types can be used depending on the situation.

When I use Intruder again, I will already have experience configuring payload positions, selecting attack types, analyzing responses, and understanding how automated request testing works.