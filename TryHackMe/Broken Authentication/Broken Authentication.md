 # Broken Authentication

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Broken Authentication  
**Date Completed:** September 11, 2026  
**Difficulty:** Medium  
**Category:** Web Application Security / Authentication Attacks  
**Room Type:** Mixed — Reading + Hands-on  

---

# Objective

The objective of this room was to understand common broken authentication vulnerabilities, including enumerating valid usernames through differences in application responses, testing login forms for brute-force weaknesses, and identifying and exploiting parameter pollution flaws within authentication mechanisms.

---

# Why Broken Authentication Matters

Authentication is the process a web application uses to verify that a user is who they claim to be.

Broken authentication occurs when weaknesses within authentication mechanisms allow an attacker to potentially abuse or bypass the intended process used to verify users.

Authentication security involves more than just the login page.

```text
Authentication Security
│
├── Login
├── Registration
├── Password Reset
├── Account Recovery
└── Other Authentication Functions
```

An application could have a secure login form but still contain weaknesses within another authentication feature, such as its password-reset functionality.

This room demonstrated why penetration testers need to examine the entire authentication process instead of only testing usernames and passwords against the login page.

---

# Key Concepts

## Authentication

Authentication verifies the identity of a user.

A basic authentication process can be represented as:

```text
User
  ↓
Provides Credentials
  ↓
Web Application
  ↓
Verifies Credentials
  ↓
Authentication Successful / Failed
```

Authentication should not be confused with session management.

```text
Authentication
→ Verifies who the user is

Session Management
→ Maintains the user's authenticated state afterward
```

Understanding this distinction was important because my previous room focused on Session Management, while this room focused more specifically on weaknesses within authentication mechanisms.

---

# Broken Authentication

Broken authentication occurs when weaknesses in a web application's authentication mechanisms allow an attacker to potentially abuse or bypass the process used to verify users.

These weaknesses can potentially exist within:

- Login functionality
- Registration functionality
- Password-reset functionality
- Account recovery
- Username handling
- Other authentication-related features

Initially, I thought of broken authentication mainly as a badly coded login form.

During my review, I learned that broken authentication is broader and can involve weaknesses throughout the application's authentication process.

---

# Username Enumeration

Username enumeration is the process of determining whether valid usernames or accounts exist within an application.

An application may unintentionally reveal this information by responding differently depending on whether a username exists.

Conceptually:

```text
Test Username
     ↓
Web Application
     ↓
Application Response
     ↓
Compare Result
     ↓
Potential Valid Username Identified
```

During the hands-on portion, I used automated testing to submit different username values and analyze the application's results.

When a valid username was tested, the result differed in a way that allowed me to identify it as a potential valid account.

I do not remember the exact response characteristic that distinguished the valid username, so I would need additional practice to become more comfortable analyzing these differences.

---

# Why Username Enumeration Matters

Username enumeration can provide useful information during an authorized penetration test because it can identify potential valid accounts within an application.

This can reduce the number of unknown values during later authentication testing.

```text
Username Enumeration
        ↓
Identify Potential Valid Account
        ↓
Known Username
        ↓
Further Authentication Testing
```

For example, a valid username could potentially be used when evaluating whether an application properly protects against password guessing or brute-force authentication attempts.

---

# Brute-Force Authentication Testing

Brute-force authentication testing involves attempting multiple credential values against an authentication mechanism to determine whether a valid combination can be found.

A simplified workflow is:

```text
Potential Valid Username
        ↓
Password Candidates
        ↓
Authentication Attempts
        ↓
Analyze Responses
        ↓
Determine Whether
Credentials Are Valid
```

A wordlist can be used to provide potential password values, although brute-force authentication testing does not always require a wordlist.

The room helped demonstrate how username enumeration and password testing can be connected.

```text
Username Enumeration
        ↓
Potential Valid Username
        ↓
Password Testing
        ↓
Authentication Result
```

This also demonstrates why applications should have protections against excessive automated authentication attempts.

---

# ffuf

During the hands-on portion, I used `ffuf`.

ffuf is a web fuzzing tool that can take input values, such as values from a wordlist, insert them into a selected location within a web request, and send multiple HTTP requests to a target application.

A simplified workflow is:

```text
Wordlist
   ↓
ffuf
   ↓
Insert Different Values
   ↓
Send HTTP Requests
   ↓
Application Responses
   ↓
Analyze Differences
```

In this room, I used ffuf while testing usernames against the web application.

The general process was:

```text
Username Wordlist
       ↓
ffuf
       ↓
Different Username Values
       ↓
HTTP Requests
       ↓
Web Application
       ↓
Responses
       ↓
Potential Valid Username
```

I found ffuf challenging because I am still becoming comfortable with its commands and understanding exactly how the generated HTTP requests are being sent.

However, I understood the overall purpose of using the tool to automate web application testing with multiple input values.

---

# curl

I also used `curl` during the room.

curl is a command-line tool that can send requests to URLs and display the responses returned by web servers.

Conceptually:

```text
Terminal
   ↓
curl
   ↓
HTTP Request
   ↓
Web Application
   ↓
HTTP Response
   ↓
Terminal
```

curl can also be used to customize parts of an HTTP request, making it useful when investigating how an application processes user-controlled parameters.

During this room, I used curl while investigating the application's password-reset functionality.

I found curl challenging because I am still becoming familiar with constructing and modifying HTTP requests from the command line.

---

# Password-Reset Functionality

One of the most important lessons from this room was that password-reset functionality is part of the authentication system.

An application could potentially have a secure normal login process while still having vulnerable password-recovery functionality.

Conceptually:

```text
Authentication Security
        ↓
   ┌────┴────┐
   ↓         ↓
Login     Password Reset
   ↓         ↓
Both Must Be Secure
```

If password-reset functionality can be manipulated, it could potentially undermine protections implemented on the normal login page.

This is why password-reset and account-recovery functionality should be examined during an authorized web application penetration test.

---

# Password-Reset Request Manipulation

During the hands-on exercise, I investigated the application's password-reset functionality using curl.

I modified an email parameter within the lab request to use an email address that I controlled.

The application processed the manipulated request and sent the password-reset information to the controlled email address.

The general behavior I observed was:

```text
Password-Reset Request
        ↓
Inspect Request Parameters
        ↓
Modify Email Parameter
        ↓
Use Email Address I Control
        ↓
Send Modified Request
        ↓
Application Processes Request
        ↓
Reset Information Sent
to Controlled Email
```

This demonstrated how insecure request handling within password-reset functionality can create authentication vulnerabilities.

I found this exercise especially interesting because I could see how modifying information within an HTTP request changed the application's behavior.

---

# Parameter Pollution

Parameter pollution was part of the room, but I did not independently remember the details of this concept during my review.

The hands-on password-reset exercise involved manipulating request parameters and observing how the application processed the modified information.

I would need additional practice with parameter pollution to confidently explain its exact mechanics and identify different implementations without guidance.

For this reason, I am not treating parameter pollution as one of the concepts I fully understood from this room yet.

---

# HTTP Requests and Authentication

Authentication testing connects directly with HTTP communication.

Common web traffic uses:

```text
HTTP  → TCP Port 80
HTTPS → TCP Port 443
```

When interacting with authentication functionality, the browser or command-line tool sends HTTP requests to the web application.

```text
Client
  ↓
HTTP/HTTPS Request
  ↓
Authentication Endpoint
  ↓
Application Processes Input
  ↓
HTTP/HTTPS Response
  ↓
Client Analyzes Result
```

Tools such as ffuf and curl ultimately interact with this same request-and-response process.

---

# How ffuf and curl Relate to HTTP

Although ffuf and curl perform different tasks, both helped me interact with HTTP requests.

```text
ffuf
→ Automates web fuzzing
→ Inserts different input values
→ Sends many HTTP requests
→ Helps compare results


curl
→ Command-line HTTP client
→ Sends HTTP requests
→ Displays responses
→ Can customize request information
```

Understanding what these tools are doing at the HTTP level is more important than simply memorizing commands.

This is an area I want to continue improving.

---

# Hands-On Walkthrough

During the hands-on portion, I practiced testing authentication functionality using ffuf and curl.

My overall workflow was:

```text
Identify Authentication Function
          ↓
Test Username Values
          ↓
Use ffuf With Wordlist
          ↓
Analyze Application Results
          ↓
Identify Potential Valid Username
          ↓
Investigate Password Reset
          ↓
Use curl
          ↓
Modify Request Information
          ↓
Change Email Parameter
          ↓
Send Modified Request
          ↓
Observe Application Behavior
```

First, I used ffuf with a wordlist to test username values against the application.

When a valid username was tested, the results allowed me to distinguish it from the other values.

I do not remember exactly what response characteristic identified the username, but I understood that differences in application responses could reveal whether an account existed.

I then used curl while investigating the password-reset functionality.

During this exercise, I modified the email parameter to use an email address I controlled within the authorized lab.

The application processed the manipulated request and sent the password-reset information to the controlled email address.

This helped demonstrate that authentication security includes more than the normal login page.

---

# Security Implications

Weak authentication mechanisms can potentially expose user accounts and sensitive application functionality.

Potential security issues include:

- Valid username disclosure
- Automated password guessing
- Weak brute-force protections
- Insecure password-reset functionality
- Improper handling of authentication parameters
- Authentication logic weaknesses
- Potential unauthorized account access

The overall lesson is:

```text
Weak Authentication Implementation
          ↓
Information Disclosure
          ↓
Authentication Testing
          ↓
Potential Authentication Abuse
          ↓
Possible Account Security Impact
```

The exact impact depends on the vulnerability and how the application implements authentication.

---

# Defensive Concepts

I did not independently remember the specific defenses discussed during the room.

During my review, I reinforced several defensive concepts related to the vulnerabilities I practiced.

## Reducing Username Enumeration

Authentication-related responses should avoid unnecessarily revealing whether specific accounts exist.

Applications should be designed so that response behavior does not make account enumeration unnecessarily easy.

## Brute-Force Protection

Applications should implement protections against excessive automated authentication attempts.

The exact protections depend on the application's design and security requirements.

## Secure Password Reset

Password-reset functionality should securely validate requests and ensure that user-controlled parameters cannot redirect or improperly alter the intended account-recovery process.

The important lesson is that password-reset functionality must receive the same security attention as the normal login mechanism.

---

# Limitations

The hardest parts of this room were using ffuf and curl.

I understood the overall purpose of the exercises, but some of the commands and HTTP request manipulation were difficult.

The areas I need additional practice with include:

- ffuf syntax and options
- curl syntax and options
- Constructing HTTP requests from the command line
- Understanding response differences
- Parameter pollution
- Recognizing authentication vulnerabilities without guidance
- Understanding how different request parameters affect server-side behavior

I also did not independently remember the specific authentication defenses from the room and reviewed those concepts afterward.

More hands-on practice will help me become more comfortable with these tools and techniques.

---

# What I Learned

From this room, I learned:

- What broken authentication means
- Why authentication security extends beyond the login page
- How username enumeration works
- Why identifying valid usernames can matter
- How brute-force authentication testing works
- How username enumeration can connect to password testing
- How ffuf can automate web fuzzing
- How wordlists can be used during authentication testing
- How curl interacts with web applications
- How HTTP requests can be modified
- Why password-reset functionality must be tested
- How insecure request handling can create authentication vulnerabilities
- Why authentication and session management are related but different
- Why understanding HTTP requests is important during web penetration testing

---

# Real-World Application

During future authorized web application penetration tests, I can apply what I learned from this room when evaluating authentication functionality.

A basic methodology I can continue developing is:

```text
Identify Authentication Functions
          ↓
Examine Application Behavior
          ↓
Look for Information Leakage
          ↓
Test for Username Enumeration
          ↓
Evaluate Authentication Controls
          ↓
Inspect HTTP Requests
          ↓
Examine Password-Reset Functionality
          ↓
Modify Controlled Parameters
When Appropriate
          ↓
Observe Application Responses
          ↓
Determine Security Impact
```

This room helped me understand that authentication testing should include more than trying credentials against a login page.

Registration, password resets, account recovery, and other authentication-related functionality can also contain vulnerabilities.

---

# Interview Notes

### What is authentication?

Authentication is the process an application uses to verify that a user is who they claim to be.

### What is broken authentication?

Broken authentication occurs when weaknesses within an application's authentication mechanisms allow the intended authentication process to potentially be abused or bypassed.

### What is username enumeration?

Username enumeration is the process of determining valid user accounts by observing differences in how an application responds to different username inputs.

### Why is username enumeration a security concern?

Identifying valid usernames can reduce uncertainty during further authentication testing and provide potential account names for password-related attacks.

### What is brute-force authentication testing?

Brute-force authentication testing involves attempting multiple credential values against an authentication mechanism to determine whether a valid combination can be found.

### What is ffuf?

ffuf is a web fuzzing tool that can automate HTTP requests while inserting different input values, such as values from a wordlist, into selected parts of a request.

### What is curl?

curl is a command-line tool used to send requests to URLs and view the responses returned by servers. It can also be used to customize HTTP requests.

### Why should password-reset functionality be tested?

Password-reset functionality is part of the authentication system. A weakness in account recovery could potentially undermine security protections implemented on the normal login page.

### What is the difference between authentication and session management?

Authentication verifies the identity of a user, while session management maintains the user's authenticated state across subsequent interactions with the application.

---

# Key Takeaway

The biggest takeaway from this room was learning that authentication security involves much more than the login form.

```text
Authentication
│
├── Login
├── Registration
├── Username Handling
├── Password Reset
└── Account Recovery
```

A weakness in any of these mechanisms can potentially affect the security of user accounts.

I also learned a basic authentication-testing workflow:

```text
Find Authentication Function
        ↓
Analyze Application Behavior
        ↓
Enumerate Potential Accounts
        ↓
Test Authentication Controls
        ↓
Inspect HTTP Requests
        ↓
Manipulate Controlled Parameters
        ↓
Observe Server Behavior
        ↓
Determine Security Impact
```

The room also reinforced how important understanding HTTP is for web penetration testing because tools such as ffuf and curl ultimately interact with web applications by sending and receiving HTTP requests.

---

# Skills Developed

- Broken Authentication Fundamentals
- Username Enumeration
- Authentication Testing
- Brute-Force Testing Fundamentals
- ffuf Fundamentals
- curl Fundamentals
- Wordlist-Based Web Fuzzing
- HTTP Request Analysis
- HTTP Response Analysis
- Request Parameter Manipulation
- Password-Reset Security Testing
- Authentication Logic Analysis
- Web Application Security Testing
- Authentication vs Session Management Understanding

---

# Screenshots

Useful screenshots from this room could include:

- Authentication page used during testing
- ffuf username enumeration results
- Valid username result with sensitive information redacted
- curl request and response
- Password-reset functionality
- HTTP request parameters being examined
- Result of the authorized password-reset exercise

Before uploading screenshots to a public GitHub repository, sensitive information such as credentials, tokens, session identifiers, reset links, email addresses, flags, and lab answers should be redacted.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was that failing to follow secure authentication practices can create vulnerabilities that allow application functionality to be manipulated.

The password-reset exercise demonstrated how insecure request handling could potentially cause sensitive reset information to be sent somewhere it was not intended to go.

This helped me understand why authentication security needs to cover the entire authentication process instead of only the login page.

## Why Broken Authentication Matters

Understanding broken authentication is important during web penetration testing because weaknesses in authentication mechanisms can potentially be manipulated to bypass intended security controls or compromise user accounts.

Identifying these weaknesses helps determine whether the application securely verifies and protects its users.

## Most Interesting Concept

The most interesting part of the room was using curl during the password-reset exercise.

I found it interesting that modifying information within an HTTP request could change how the application processed the password-reset functionality.

This helped demonstrate how insecure request handling can create authentication vulnerabilities and made me more interested in understanding HTTP requests from the command line.

## Future Penetration Tests

This room will help me during future web penetration tests because I now have a better understanding of how to identify and test authentication vulnerabilities.

I can apply what I learned about username enumeration, login testing, HTTP request manipulation, and password-reset functionality when examining authentication mechanisms during future authorized web application tests.

I also want to continue practicing ffuf and curl so I can become more comfortable understanding exactly how the tools construct and send HTTP requests.