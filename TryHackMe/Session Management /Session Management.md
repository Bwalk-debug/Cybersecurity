 # Session Management

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Session Management  
**Date Completed:** September 10, 2026  
**Difficulty:** Medium  
**Category:** Web Application Security / Session Management  
**Room Type:** Mixed — Mostly Reading + Hands-on  

---

# Objective

The objective of this room was to better understand how web applications manage user interactions and track a user's actions across multiple requests. I also learned how session management is implemented and about different attacks that can be performed against insecure session management implementations.

---

# Why Session Management Matters

HTTP is stateless, meaning individual HTTP requests do not inherently remember previous requests.

Because users interact with web applications across many different requests, applications need a way to maintain information about a user's interaction.

A simplified example is:

```text
User Logs In
     ↓
Session Established
     ↓
User Requests Profile
     ↓
Application Recognizes Session
     ↓
User Requests Settings
     ↓
Application Continues Recognizing Session
```

Session management allows the application to associate multiple requests with the appropriate user's ongoing session.

This becomes especially important after authentication because session-related credentials can become security-sensitive.

---

# Key Concepts

## Sessions

A session allows a web application to maintain information about a user's interaction with the application across multiple HTTP requests.

Initially, I confused a session with the request being made to the server.

During my review, I clarified the difference:

```text
HTTP Request
→ A browser asks the server/application for something.

Session
→ Allows the application to maintain state across requests.
```

For example:

```text
Browser
   ↓
Login Request
   ↓
Application Authenticates User
   ↓
Session Established
   ↓
Additional Requests
   ↓
Application Associates Requests
With Existing Session
```

Understanding this distinction helped me better understand the rest of the room.

---

# HTTP Is Stateless

During my review, I clarified that HTTP is stateless.

This means that individual HTTP requests do not inherently remember previous requests.

For example:

```text
Request 1 → Login

Request 2 → Profile

Request 3 → Account Settings

Request 4 → Dashboard
```

Session management provides a mechanism for the web application to maintain state across these interactions.

A simplified flow is:

```text
Browser                     Web Application
   │                               │
   │──── HTTP Request ────────────→│
   │                               │
   │←──── HTTP Response ───────────│
   │                               │
   │──── Another Request ─────────→│
   │                               │
```

Session-related information can help the application determine that these requests belong to the same ongoing user interaction.

---

# Cookies, Tokens, and Session Identifiers

Cookies and tokens can be involved in session management.

Depending on how the application is designed, a browser may store a cookie containing or representing a session identifier.

Conceptually:

```text
User Authenticates
       ↓
Session Established
       ↓
Browser Receives/Holds
Session-Related Value
       ↓
Future HTTP Requests
Include Applicable Value
       ↓
Application Recognizes Session
```

An important concept I learned is that a session cookie does not necessarily contain the user's username and password.

Instead, it may contain a value that represents or identifies an authenticated session.

Because of this, session-related values can be security-sensitive.

---

# HTTP Headers

One of the most interesting parts of this room was inspecting HTTP headers.

During the hands-on exercises, I observed cookie information within HTTP headers.

A simplified HTTP request could contain information such as:

```text
HTTP Request
│
├── Method / Path
├── Headers
│   ├── Host
│   ├── Cookie
│   └── Other Headers
│
└── Request Body (when applicable)
```

Conceptually:

```text
Browser
   │
   │ HTTP Request
   │
   │ Headers:
   │ Cookie: session=...
   │
   ▼
Web Application
```

The server can also send cookie-related instructions back to the browser through HTTP response headers such as `Set-Cookie`.

Examining these headers helped me begin connecting browser behavior, HTTP communication, cookies, and session management.

---

# Cookie Security Attributes

## Secure

The `Secure` cookie attribute instructs the browser to send the cookie only over HTTPS connections.

```text
Cookie with Secure Attribute

HTTP  → Not sent
HTTPS → Sent when applicable
```

This helps prevent the cookie from being transmitted over an unencrypted HTTP connection.

The `Secure` attribute does not protect a cookie from every possible attack. Its purpose is specifically related to preventing transmission over ordinary unencrypted HTTP connections.

---

## HttpOnly

The `HttpOnly` cookie attribute prevents client-side JavaScript from accessing the cookie through normal browser scripting interfaces.

Conceptually:

```text
Cookie Without HttpOnly
        ↓
Client-Side JavaScript
May Be Able to Access It


Cookie With HttpOnly
        ↓
Client-Side JavaScript
Cannot Normally Read It
```

This connects with what I previously learned about Cross-Site Scripting.

If an XSS vulnerability exists, `HttpOnly` can help prevent an HttpOnly session cookie from being directly read through injected client-side JavaScript.

However:

```text
HttpOnly
    ≠
Prevention for XSS itself
```

It is an additional cookie protection.

---

## SameSite

I did not independently remember how the `SameSite` cookie attribute worked during this room review.

During my review, I clarified that `SameSite` controls certain situations where browsers include cookies with requests involving other sites or cross-site contexts.

At a high level:

```text
SameSite=Strict
→ Most restrictive cross-site behavior

SameSite=Lax
→ Allows cookies in some cross-site situations

SameSite=None
→ Allows cross-site cookie use
→ Used with Secure in modern browsers
```

This can be relevant when reducing certain Cross-Site Request Forgery risks.

---

# Session Hijacking

Session hijacking was one of the attacks I remembered from the room.

Session hijacking occurs when an attacker obtains a user's valid session identifier or another session credential and abuses it to access or act within the victim's authenticated session.

Conceptually:

```text
Victim Authenticates
       ↓
Valid Session Established
       ↓
Attacker Obtains
Valid Session Credential
       ↓
Attacker Uses Credential
       ↓
Application May Associate
Attacker's Requests With
Victim's Session
```

An important concept is that an attacker abusing a valid authenticated session credential may not necessarily need to know the victim's password.

This demonstrates why session identifiers and other session credentials need to be protected.

---

# Session Fixation

I did not independently remember session fixation during the room review, so I reviewed the concept afterward.

Session fixation involves an attacker getting a victim to use a session identifier that the attacker already knows.

A simplified flow is:

```text
Attacker Knows Session ID
        ↓
Victim Uses That Session
        ↓
Victim Authenticates
        ↓
Application Fails to Properly
Regenerate Session Identifier
        ↓
Previously Known Session
May Remain Valid
```

One important defensive concept is regenerating session identifiers after authentication or important privilege changes.

---

# Session Prediction

I also did not independently remember session prediction during the review.

I clarified that session prediction can become possible when an application generates session identifiers in an insecure or predictable manner.

For example, an insecure design could theoretically use an obvious pattern:

```text
Session 1 → 10001
Session 2 → 10002
Session 3 → 10003
```

If session identifiers were predictable, an attacker could potentially attempt to determine other valid session values.

Session identifiers should therefore be generated with sufficient randomness and entropy so that valid values cannot practically be predicted.

---

# Session Logout and Invalidation

Another important concept I reviewed was what should happen when a user logs out.

Initially, I understood that the browser should no longer have access to the previous session cookie.

However, I learned that removing the browser cookie is not necessarily the same as invalidating the authenticated session.

A secure logout process should ensure that the old authenticated session can no longer be used.

Conceptually:

```text
User Logged In
      ↓
Valid Session
      ↓
User Logs Out
      ↓
Session Invalidated
      ↓
Associated Cookie Removed
or Expired When Appropriate
      ↓
Old Session Credential
Should No Longer Work
```

This prevents a previous session credential from continuing to provide authenticated access after logout.

---

# Networking Concepts

Session management connects directly with networking concepts because session-related information is exchanged through HTTP/HTTPS communication.

Common web communication uses:

```text
HTTP  → TCP Port 80
HTTPS → TCP Port 443
```

A simplified flow is:

```text
Browser
   ↓
HTTP/HTTPS Request
   ↓
Request Headers
   ↓
Cookie / Session Information
   ↓
Web Application
   ↓
Session Processing
   ↓
HTTP/HTTPS Response
   ↓
Browser
```

Cookies can be included within applicable HTTP request headers, while the application can send cookie-related instructions through response headers.

HTTPS is particularly important because it encrypts HTTP communication while it travels between the client and server.

The `Secure` cookie attribute helps ensure that a cookie is only transmitted over HTTPS when applicable.

---

# Hands-On Walkthrough

During the hands-on portion of the room, I created a user account on a web application and navigated through different parts of the website.

I then used browser inspection tools to examine requests and cookies associated with my interactions.

My general workflow was:

```text
Create User
     ↓
Interact With Website
     ↓
Inspect Requests
     ↓
Inspect HTTP Headers
     ↓
Examine Cookies
     ↓
Remove Cookies
     ↓
Observe Application Behavior
```

Removing cookies helped demonstrate that the browser's session-related information affects how the application recognizes the user's session.

I initially thought removing the session cookie would remove information I had provided to the website.

During my review, I clarified that deleting a session cookie from the browser does not necessarily delete the user's account, application data, or server-side session information immediately.

Instead, removing a session-related cookie may prevent the application from associating future browser requests with the previous session.

This could cause the user to appear logged out or lose access to session-specific functionality.

Some portions of the hands-on exercise were confusing, so I referenced some of the provided material and answers while completing the room.

Reviewing the concepts afterward helped me better understand what I was observing.

---

# Session Management Security

Secure session management is important because weaknesses in how sessions are created, protected, maintained, or invalidated could potentially allow an attacker to abuse another user's authenticated session.

Important security concepts include:

- Protecting session credentials
- Using sufficiently unpredictable session identifiers
- Using HTTPS
- Using appropriate cookie security attributes
- Regenerating session identifiers when appropriate
- Properly invalidating sessions during logout
- Protecting authenticated sessions from unauthorized use

The overall security relationship can be represented as:

```text
User Authenticates
       ↓
Session Established
       ↓
Session Credential Issued
       ↓
Credential Must Be Protected
       ↓
Application Uses Credential
To Recognize Authenticated Session
```

If that credential becomes compromised or session management is implemented insecurely, the authenticated session could potentially be abused.

---

# Limitations

This room was more difficult for me because I initially found some of the session-management concepts confusing.

The hands-on portion was especially challenging because I could see HTTP requests, headers, and cookies but did not completely understand everything I was looking at.

I had to reference some answers and room material during the exercises.

The concepts I needed additional clarification on included:

- Why HTTP requires session management
- The difference between requests and sessions
- What happens when a session cookie is removed
- Session fixation
- Session prediction
- SameSite cookies
- Proper session invalidation during logout

I became more comfortable with these concepts during my review, but they are areas I need to continue practicing.

---

# What I Learned

From this room, I learned:

- What a web session is
- Why web applications need session management
- That HTTP is stateless
- The difference between an HTTP request and a session
- How cookies and tokens can relate to sessions
- Why session credentials are security-sensitive
- How cookies can appear within HTTP headers
- How the `Secure` cookie attribute works
- How the `HttpOnly` cookie attribute works
- The purpose of the `SameSite` attribute
- How session hijacking works
- The basic concepts behind session fixation
- The basic concepts behind session prediction
- Why unpredictable session identifiers are important
- Why authenticated sessions should be invalidated during logout
- Why deleting a browser cookie does not necessarily delete server-side data
- How browser behavior, HTTP requests, cookies, and sessions connect

---

# Real-World Application

During future authorized web application penetration tests, I can use what I learned from this room to better understand how an application manages authenticated users.

A basic methodology I can continue developing is:

```text
Authenticate to Application
        ↓
Observe Session Behavior
        ↓
Inspect HTTP Requests
        ↓
Inspect Headers
        ↓
Identify Session-Related Values
        ↓
Examine Cookie Protections
        ↓
Observe Session Lifecycle
        ↓
Investigate Potential
Session Management Weaknesses
```

As I gain more experience, understanding sessions will help me make better sense of authentication behavior and the HTTP traffic I inspect during web application testing.

---

# Interview Notes

### What is a session?

A session allows a web application to maintain information about a user's interaction with the application across multiple HTTP requests.

### Why do web applications need sessions?

HTTP is stateless, meaning individual requests do not inherently remember previous requests. Session management allows an application to maintain state across a user's interactions.

### What is a session identifier?

A session identifier is a value that can be used by an application to associate requests with a particular session.

### Are session cookies the same as usernames and passwords?

No. A session cookie does not necessarily contain the user's username and password. It may instead contain or represent a value used to identify an existing session.

### Why are session credentials sensitive?

If an attacker obtains a valid authenticated session credential and the application lacks sufficient protections, the credential could potentially be abused to act within the user's session.

### What is session hijacking?

Session hijacking occurs when an attacker obtains and abuses another user's valid session credential to access or act within the victim's authenticated session.

### What does the Secure cookie attribute do?

The `Secure` attribute instructs the browser to send the cookie only over HTTPS connections.

### What does HttpOnly do?

`HttpOnly` prevents client-side JavaScript from accessing the cookie through normal browser scripting interfaces.

### What does SameSite do?

`SameSite` controls certain situations in which browsers include cookies with cross-site requests and can help reduce certain CSRF risks.

### What should happen when a user logs out?

The authenticated session should be invalidated so that the previous session credential can no longer be used. The associated browser cookie should also be removed or expired when appropriate.

---

# Key Takeaway

The biggest takeaway from this room was gaining a better understanding of how sessions work and why they are necessary for web applications.

The main mental model I learned is:

```text
HTTP Is Stateless
       ↓
Application Needs Session Management
       ↓
User Authenticates
       ↓
Session Established
       ↓
Browser Holds Session-Related Value
       ↓
Value Can Be Sent in HTTP Headers
       ↓
Application Associates Requests
With the Correct Session
```

I also learned why protecting session credentials is important:

```text
Session Credential
       ↓
Represents/Identifies Session
       ↓
Application Trusts Valid Credential
       ↓
Credential Must Be Protected
       ↓
Compromise Could Lead to
Session Abuse
```

---

# Skills Developed

- Session Management Fundamentals
- HTTP Session Understanding
- HTTP Request Analysis
- HTTP Header Inspection
- Cookie Analysis
- Session Identifier Awareness
- Session Hijacking Fundamentals
- Session Fixation Awareness
- Session Prediction Awareness
- Secure Cookie Attribute Understanding
- HttpOnly Cookie Attribute Understanding
- SameSite Awareness
- Session Lifecycle Understanding
- Authentication and Session Security
- Web Application Security Testing

---

# Screenshots

Useful screenshots from this room could include:

- User account created within the lab
- Browser developer tools showing HTTP requests
- HTTP request headers
- Cookie information
- Session-related cookie values with sensitive values redacted
- Cookie security attributes
- Application behavior before and after removing a session-related cookie

Before uploading screenshots to a public GitHub repository, sensitive session values, credentials, flags, tokens, and lab answers should be redacted.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was gaining a better understanding of sessions and how web applications use session management to maintain information about a user's interactions across multiple HTTP requests.

At the beginning of the room, some of these concepts were confusing, but reviewing them helped me better understand the relationship between HTTP requests, cookies, and sessions.

## Why Session Management Matters

Understanding sessions and cookies is important during web penetration testing because I need to understand the terminology, how these mechanisms work, and how web applications maintain authenticated user sessions.

This knowledge can help me better understand application behavior and recognize potential weaknesses in how sessions are managed.

## Most Interesting Concept

The part that interested me the most was inspecting the HTTP headers.

Even though I did not completely understand everything I was looking at yet, seeing the information contained within the requests grabbed my attention.

I especially found it interesting seeing cookies within the headers and beginning to understand how they relate to session management.

This is an area I want to continue practicing as I perform more web application labs.

## Future Penetration Tests

This room will help me during future web penetration tests because I will be more familiar with sessions, cookies, and HTTP headers when I encounter them again.

As I continue practicing web application testing, I will be able to build on these fundamentals and better understand how applications manage authenticated users.