 # CSRF Introduction

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** CSRF Introduction  
**Date Completed:** August 29, 2026  
**Difficulty:** Easy  
**Category:** Web Application Security / Cross-Site Request Forgery (CSRF)  
**Room Type:** Mixed — Mainly Reading + Light Hands-on  

---

# Objective

The objective of this room was to understand how Cross-Site Request Forgery (CSRF) works, how it can abuse a user's authenticated session to perform unintended actions, and how to identify potential CSRF vulnerabilities during web application security testing.

---

# Why CSRF Matters

Cross-Site Request Forgery is an important web application vulnerability because it can cause an authenticated user's browser to perform actions that the user did not intend to perform.

One of the biggest things I learned was that CSRF is not primarily about stealing a user's credentials or session cookie. Instead, an attacker attempts to abuse the victim's existing authenticated session by causing their browser to send an unintended request to the legitimate application.

Potential state-changing actions could include:

- Changing an email address
- Changing a password
- Modifying account settings
- Changing payment-related information
- Performing other sensitive account actions

---

# Key Concepts

## Cross-Site Request Forgery (CSRF)

CSRF is a web application vulnerability where an attacker causes an authenticated user's browser to send an unintended request to a legitimate web application.

If the application does not properly verify that the user intended to perform the action, it may process the request using the victim's authenticated session.

A simple way to remember CSRF is:

> **CSRF tricks an authenticated user's browser into performing an action that the user did not intend to perform.**

---

## State-Changing Requests

State-changing requests modify information or perform an action within an application.

Examples include:

- Changing an email address
- Changing a password
- Modifying account settings
- Changing payment information

These requests are important during CSRF testing because they can potentially cause meaningful changes to a victim's account.

Finding a state-changing request does not automatically mean the application is vulnerable. The application's CSRF protections must also be examined.

---

## Cookies and Authenticated Sessions

Cookies and authenticated sessions are important for understanding CSRF.

A session cookie can help the server associate incoming requests with an authenticated user's session.

One concept I initially misunderstood was thinking that CSRF required the attacker to steal the victim's cookie or credentials.

The attacker does not necessarily need to know or steal the victim's session cookie. Instead, depending on the cookie configuration and request context, the browser may automatically include the appropriate session information when communicating with the legitimate application.

The basic concept is:

```text
Victim's Browser
       ↓
Authenticated Session Exists
       ↓
Unwanted Request Is Triggered
       ↓
Request Goes to Legitimate Application
       ↓
Session Information May Be Included
       ↓
Application Recognizes Victim
```

This existing authenticated relationship between the browser and the application is what CSRF attempts to abuse.

---

## CSRF Tokens

A CSRF token is a security value used by a web application to help verify that a state-changing request came through the expected legitimate application workflow.

A simplified process is:

```text
Application Provides CSRF Token
              ↓
User Performs Legitimate Action
              ↓
Request Contains Token
              ↓
Server Validates Token
              ↓
Valid → Request Processed
Invalid/Missing → Request Rejected
```

During CSRF testing, it is important to determine whether CSRF tokens are present and whether the application properly validates them.

The existence of a token alone does not necessarily mean the application is protected if the token is not properly enforced.

---

# How CSRF Works

A simplified CSRF attack flow looks like this:

```text
Victim Logs Into Legitimate Application
                ↓
Browser Has an Authenticated Session
                ↓
Victim Encounters Attacker-Controlled Content
                ↓
Malicious Content Triggers a Request
                ↓
Victim's Browser Sends the Request
                ↓
Legitimate Application Receives the Request
                ↓
Application Associates It With Victim's Session
                ↓
Unintended Action May Be Performed
```

An important concept I learned is that the attacker does not necessarily need to steal the victim's credentials or session cookie.

Instead, the attacker attempts to make the victim's already-authenticated browser perform the unwanted action.

---

# Networking Concepts

## HTTP and HTTPS

CSRF relies heavily on understanding how browsers communicate with web applications through HTTP requests.

Common web protocols include:

```text
HTTP  → TCP Port 80
HTTPS → TCP Port 443
```

A normal web communication flow looks like:

```text
Browser
   ↓
HTTP/HTTPS Request
   ↓
Web Application
   ↓
Application Processes Request
   ↓
HTTP/HTTPS Response
   ↓
Browser
```

During a CSRF scenario, attacker-controlled content attempts to cause the victim's browser to generate an unintended HTTP request.

HTTPS protects communication while it travels across the network, but HTTPS alone does not prevent CSRF because the vulnerability concerns whether the application properly validates the legitimacy of the request.

---

## CSRF Request Flow

Understanding the request flow was one of the most important concepts for me in this room.

```text
ATTACKER
Creates Attacker-Controlled Content
             ↓
VICTIM
Already Authenticated to Application
             ↓
VICTIM'S BROWSER
Interacts With Malicious Content
             ↓
FORGED REQUEST
Browser Sends Unintended Request
             ↓
LEGITIMATE APPLICATION
Receives Request Under Victim's Session
             ↓
STATE-CHANGING ACTION
May Be Performed
```

The attacker does not necessarily need the victim's:

- Password
- Session cookie value
- Account credentials

Instead, CSRF attempts to abuse the victim's existing authenticated browser session.

---

# Hands-On Walkthrough

The hands-on portion demonstrated the relationship between attacker-controlled content, the victim's browser, and the legitimate web application.

I created an attacker-controlled file designed to cause the victim's browser to perform an unintended request.

The basic process was:

```text
Attacker-Controlled File
          ↓
Victim Interacts With Content
          ↓
Victim's Browser
          ↓
Unintended Request
          ↓
Legitimate Application
          ↓
Request Processed Using
Victim's Authenticated Context
```

Initially, I had difficulty understanding where the request was actually being sent.

I first thought the attacker-controlled file was primarily capturing the victim's request. After reviewing the process, I better understood that the attacker-controlled content can trigger the victim's browser to send an unintended request to the legitimate vulnerable application.

This helped me understand the actual request flow involved in CSRF.

---

# Identifying Potential CSRF Vulnerabilities

When investigating a web application for potential CSRF vulnerabilities, I learned to:

1. Analyze HTTP requests made by the application.
2. Identify requests that perform state-changing actions.
3. Understand how the authenticated session is maintained.
4. Observe how cookies behave with the request.
5. Look for CSRF protections such as CSRF tokens.
6. Determine whether those protections are properly validated.

A state-changing request without adequate CSRF protection would require further investigation.

---

# Vulnerabilities / Security Implications

A successful CSRF attack can potentially cause unauthorized state-changing actions within a victim's account.

Depending on the application, the impact could include:

- Unauthorized account modifications
- Email address changes
- Password changes
- Account setting modifications
- Payment-related changes
- Other sensitive actions available to the authenticated user

The actual severity depends on what functionality is vulnerable and what permissions the victim has within the application.

---

# CSRF Prevention

## CSRF Tokens

Properly generated and validated CSRF tokens can help prevent forged requests from being successfully processed.

The server should verify that the expected token is present and valid before allowing sensitive state-changing actions.

## SameSite Cookies

The `SameSite` cookie attribute can restrict when cookies are included in cross-site requests.

The main settings include:

- `Strict` — provides strong restrictions on cross-site cookie use.
- `Lax` — allows cookies in certain cross-site navigation situations while restricting others.
- `None` — allows cross-site cookie use and is used with the `Secure` attribute in modern browsers.

This concept was clarified during my review of the room rather than something I independently remembered from the room.

## Protecting State-Changing Actions

Sensitive state-changing functionality should use appropriate security controls to ensure that requests are legitimate and intentionally initiated by the authenticated user.

---

# Limitations

The biggest challenge I experienced during this room was understanding how the request traveled between the attacker-controlled content, the victim's browser, and the legitimate application.

Initially, I associated CSRF with capturing a victim's request, credentials, or session information.

After reviewing the attack flow, I learned that CSRF does not necessarily require stealing this information.

Instead, the attacker attempts to cause the victim's authenticated browser to perform an unintended action against the legitimate application.

---

# What I Learned

From this room, I learned:

- What Cross-Site Request Forgery is.
- How CSRF works.
- How CSRF differs from credential theft.
- How CSRF differs from session theft.
- Why authenticated sessions matter during CSRF.
- Why state-changing requests are important.
- How cookies relate to authenticated requests.
- The purpose of CSRF tokens.
- How attacker-controlled content can trigger unintended requests.
- How to begin identifying potential CSRF vulnerabilities.
- Why understanding HTTP request flow is important during web penetration testing.

---

# Real-World Application

During future authorized web application penetration tests, I can use what I learned from this room to identify functionality that may need to be investigated for CSRF.

I can examine state-changing requests, determine how the application maintains the user's authenticated session, observe cookie behavior, and look for protections such as CSRF tokens.

This room also helped me understand that simply finding a sensitive request does not automatically mean the application is vulnerable. The application's protections and request validation must also be investigated.

---

# Interview Notes

### What is CSRF?

Cross-Site Request Forgery is a web application vulnerability where an attacker causes an authenticated user's browser to send an unintended request to a legitimate application.

### Does CSRF require stealing a user's credentials?

No. CSRF generally attempts to abuse the victim's existing authenticated session rather than requiring the attacker to steal the victim's username and password.

### Does CSRF require stealing the session cookie?

Not necessarily. The victim's browser may already have an authenticated session with the application and may include relevant session information when sending the request.

### Why are state-changing requests important?

State-changing requests modify information or perform actions within an application, making them important targets when investigating potential CSRF vulnerabilities.

### What is a CSRF token?

A CSRF token is a security value that a web application can validate with sensitive requests to help determine whether the request came through the expected legitimate workflow.

### How can CSRF be prevented?

CSRF protections can include properly generated and validated CSRF tokens, appropriate cookie security settings, and secure handling of sensitive state-changing functionality.

---

# Key Takeaway

The biggest takeaway from this room was understanding that CSRF is not primarily about stealing a victim's credentials or session.

Instead:

> **CSRF tricks an authenticated user's browser into performing an action that the user did not intend to perform.**

Understanding this distinction helped me better understand how HTTP requests, cookies, authenticated sessions, attacker-controlled content, and state-changing actions work together during a CSRF scenario.

---

# Skills Developed

- CSRF Fundamentals
- Web Application Security
- HTTP Request Analysis
- State-Changing Request Identification
- Cookie and Session Analysis
- CSRF Token Awareness
- Web Authentication Concepts
- Vulnerability Identification
- Web Application Penetration Testing Methodology

---

# Screenshots

Useful screenshots for this room include:

- Attacker-controlled file used during the hands-on portion
- Relevant state-changing request
- Application before the state-changing action
- Application after the state-changing action
- CSRF protections observed during testing

Sensitive information, credentials, flags, and lab answers should be redacted before uploading screenshots to a public GitHub repository.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was that CSRF is not about stealing a user's credentials or session. Instead, CSRF involves causing an authenticated user's browser to perform an action that the user did not intend to perform on a legitimate web application.

## Why This Knowledge Matters

Understanding HTTP requests, cookies, and authenticated sessions is important because it helps me understand how a web application identifies a user and processes their requests.

During CSRF testing, this knowledge helps me identify state-changing requests and determine whether the application has adequate protections against forged requests.

## Most Interesting Concept

The attacker-controlled file interested me the most because I initially had difficulty understanding how it worked.

After learning the request flow, I understood that attacker-controlled content can cause the victim's browser to send an unintended request to the legitimate application.

I found this interesting because the attacker can potentially abuse the victim's existing authenticated session without necessarily stealing the victim's credentials or session cookie.

## Future Penetration Tests

This room will help me during future web application penetration tests because it introduced me to the step-by-step process of identifying potential CSRF vulnerabilities.

I now know to examine state-changing requests, understand how the application maintains authenticated sessions, observe cookie behavior, and determine whether protections such as CSRF tokens are being used and properly validated.