 # XSS Introduction

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** XSS Introduction  
**Date Completed:** August 31, 2026  
**Difficulty:** Medium  
**Category:** Web Application Security / Cross-Site Scripting (XSS)  
**Room Type:** Mixed — Reading + Hands-on  

---

# Objective

The objective of this room was to gain a better understanding of how Cross-Site Scripting (XSS) works, learn how to identify potential XSS vulnerabilities within web applications, and understand how examining page source and application behavior can help during XSS testing.

---

# Why XSS Matters

Cross-Site Scripting is an important web application vulnerability because it can allow attacker-controlled content to execute within another user's browser in the context of a vulnerable website.

Depending on the application and its security controls, successful XSS could potentially allow an attacker to:

- Manipulate webpage content
- Access information exposed to client-side JavaScript
- Perform actions within a user's context
- Potentially contribute to session compromise
- Affect other users who interact with vulnerable content

One important concept I learned is that these are potential impacts of XSS rather than the definition of XSS itself.

The vulnerability occurs when attacker-controlled input reaches an executable browser context because the application or client-side code handles the input insecurely.

---

# Key Concepts

## Cross-Site Scripting (XSS)

Cross-Site Scripting is a web application vulnerability where attacker-controlled input is handled insecurely and results in script execution within a user's browser in the context of the vulnerable website.

A simplified flow is:

```text
Attacker-Controlled Input
          ↓
Vulnerable Web Application
          ↓
Input Reaches Browser Unsafely
          ↓
Browser Interprets Input as Code
          ↓
Attacker-Controlled JavaScript Executes
```

Successful XSS does not automatically mean that an attacker completely controls another user's account. The impact depends on what the injected JavaScript can access or perform and what security protections are implemented.

---

# HTML and JavaScript

## HTML

HTML provides the structure of a webpage.

Understanding HTML is important during XSS testing because user-controlled input can appear in different locations within the page.

For example, input could appear within:

- Normal HTML content
- HTML attributes
- Forms
- Other parts of the document

The location of the input can affect how it must be tested.

## JavaScript

JavaScript provides executable behavior within webpages and was the primary scripting language involved during the XSS exercises.

During XSS testing, the goal is to determine whether attacker-controlled input can reach a browser context where it is interpreted as executable content rather than harmless data.

A basic proof-of-concept JavaScript payload can be used during authorized testing to provide visible evidence that JavaScript execution occurred.

---

# Types of XSS

## Reflected XSS

Reflected XSS occurs when attacker-controlled input is sent to a vulnerable web application, such as through a parameter, and the application immediately includes that input within its response without safely handling it.

The general flow is:

```text
Request Contains Input
        ↓
Vulnerable Application
        ↓
Input Reflected in Response
        ↓
Browser Renders Response
        ↓
Script May Execute
```

The malicious input does not necessarily remain permanently within the application.

Instead, it is reflected through the request and response.

---

## Stored XSS

Stored XSS occurs when attacker-controlled input is saved by the application and later returned when affected content is viewed.

The general flow is:

```text
Attacker Submits Input
        ↓
Application Stores Input
        ↓
User Later Views Content
        ↓
Stored Input Is Returned
        ↓
Script May Execute
```

This differs from Reflected XSS because the malicious input persists within the application rather than only being returned through the immediate response.

Stored XSS was the XSS type that interested me the most because the attacker-controlled input can remain within the application and potentially execute later when affected content is viewed.

---

## Blind XSS

Blind XSS occurs when attacker-controlled input is submitted to an application, but the tester cannot directly observe where or when the payload executes.

Conceptually:

```text
Input Submitted
      ↓
Application Stores or Processes Input
      ↓
Tester Does Not See Execution
      ↓
Different User or Page
Processes Input Later
      ↓
Payload May Execute
```

The tester may submit the input in one location while execution occurs somewhere else.

Blind XSS can commonly involve stored input, but the important testing characteristic is that the tester does not directly observe execution at the original submission point.

---

## DOM-Based XSS

DOM-based XSS involves client-side JavaScript handling attacker-controlled data unsafely within the browser.

The DOM, or Document Object Model, is the browser's representation of the webpage that JavaScript can read and modify.

A simplified flow is:

```text
Attacker-Controlled Data
          ↓
Browser
          ↓
Client-Side JavaScript
          ↓
Unsafe DOM Handling
          ↓
Browser Interprets Data as Code
          ↓
Script Executes
```

The main concept I remembered from the room was that DOM-based XSS occurs on the client side.

Reviewing the concept helped me better understand how client-side JavaScript and the DOM are involved.

---

# Reflected Input vs XSS

An important concept from this room was learning that finding user-controlled input reflected within a webpage does not automatically prove that XSS exists.

For example:

```text
Input Submitted
      ↓
Input Appears on Page
      ↓
Input Is Reflected
```

This alone does not confirm XSS.

Instead, testing must determine whether the controlled input can reach an executable browser context.

```text
Controlled Input
      ↓
Unsafe Browser Context
      ↓
Browser Interprets Input as Code
      ↓
JavaScript Executes
      ↓
Evidence of XSS
```

This distinction helped me better understand what I am actually trying to prove during XSS testing.

---

# Viewing Page Source

Viewing the page source helped me understand where my controlled input appeared within the webpage.

This is important because input can appear in different contexts within HTML or JavaScript.

The basic testing process was:

```text
Submit Controlled Input
          ↓
Application Processes Input
          ↓
Observe Application Response
          ↓
Examine Where Input Appears
          ↓
Understand the Context
          ↓
Adapt Testing if Necessary
```

One of the important lessons from the room was that the same testing approach does not necessarily work in every situation.

The input may need to be changed depending on where it appears within the webpage and how the application handles it.

I do not remember the exact requirements for every context, but I understood why examining the source was important.

---

# Hands-On Walkthrough

During the hands-on portion of the room, I tested user-controlled inputs such as search boxes and forms.

The general methodology I practiced was:

```text
Find User-Controlled Input
          ↓
Submit Test Input
          ↓
Observe Application Behavior
          ↓
Examine Where Input Appears
          ↓
Understand Its Context
          ↓
Modify Testing When Necessary
          ↓
Determine Whether JavaScript Executes
```

I used basic proof-of-concept JavaScript testing to determine whether the application would execute attacker-controlled JavaScript.

A visible result, such as a popup, could provide evidence that the controlled input reached an executable browser context.

I also learned that the same input did not necessarily work in every situation. I had to change my testing based on how the application handled the input and where it appeared within the webpage.

I do not remember the exact syntax or requirements used for every exercise, so I would need additional practice with HTML and JavaScript to become more comfortable adapting XSS testing to different contexts.

---

# Networking Concepts

## HTTP and HTTPS

XSS occurs within web applications, making HTTP and HTTPS important networking concepts.

Common web communication uses:

```text
HTTP  → TCP Port 80
HTTPS → TCP Port 443
```

A simplified request and response flow is:

```text
Browser
   ↓
HTTP/HTTPS Request
   ↓
Web Application
   ↓
Application Processes Input
   ↓
HTTP/HTTPS Response
   ↓
Browser Renders Response
```

With Reflected XSS, attacker-controlled input can be included within a request and reflected into the application's response.

The browser then processes the returned content.

---

## Browser Execution

Understanding the difference between the server and browser is important during XSS testing.

```text
User Input
    ↓
HTTP Request
    ↓
Web Application
    ↓
HTTP Response
    ↓
Browser
    ↓
HTML / JavaScript Processing
```

The browser is responsible for interpreting the returned HTML and executing JavaScript.

This is why understanding both HTTP communication and browser behavior is important when investigating XSS.

---

# Security Impact

Successful XSS can potentially affect users of a vulnerable web application.

Depending on the application and its security controls, possible impacts could include:

- Manipulating webpage content
- Accessing information available to client-side JavaScript
- Performing unauthorized actions within a user's context
- Potentially contributing to session compromise
- Affecting users who view stored malicious content

Successful XSS does not automatically provide complete access to another user's account.

The actual impact depends on the vulnerable application, browser protections, cookie configuration, and what the injected JavaScript is capable of accessing or performing.

---

# XSS Prevention

I did not independently remember the specific XSS prevention techniques taught during the room.

During my review, I clarified that an important defense is safely handling user-controlled data so the browser treats it as data rather than executable content.

## Context-Appropriate Output Encoding

Output encoding helps ensure that special characters within user-controlled data are interpreted as data instead of executable HTML or JavaScript.

Conceptually:

```text
User-Controlled Input
          ↓
Context-Appropriate Output Encoding
          ↓
Browser Receives Safely Handled Data
          ↓
Input Treated as Data
Instead of Executable Content
```

The correct protection depends on where the data is being inserted into the webpage.

## Safe DOM Handling

Client-side JavaScript should avoid unsafe DOM operations that can cause attacker-controlled data to become executable content.

Understanding safe DOM handling is especially important when preventing DOM-based XSS.

---

# Limitations

The hardest part of this room was understanding some of the HTML and JavaScript involved in XSS because coding is currently an area where I am less confident.

XSS testing requires understanding several concepts together:

```text
HTML
→ Where does my input appear?

JavaScript
→ What code is executing?

DOM
→ How is the browser modifying the page?

Context
→ How is my input being interpreted?
```

This room showed me that improving my ability to read basic HTML and JavaScript will make it easier to understand why certain XSS techniques work in different situations.

I also do not remember the exact syntax or requirements for every XSS context, so this is an area I want to continue practicing.

---

# What I Learned

From this room, I learned:

- What Cross-Site Scripting is
- How attacker-controlled input can lead to browser-side code execution
- The difference between XSS itself and the potential impact of XSS
- How JavaScript is involved in XSS
- Why HTML is important when analyzing XSS
- The difference between Reflected and Stored XSS
- How Blind XSS works
- The client-side nature of DOM-based XSS
- How to identify user-controlled input
- How to test search boxes and forms
- Why examining page source is useful
- Why reflected input does not automatically prove XSS
- Why testing may need to change depending on the input context
- How successful JavaScript execution can provide evidence of XSS

---

# Real-World Application

During future authorized web application penetration tests, I can use what I learned from this room to better investigate potential XSS vulnerabilities.

A basic methodology I can follow is:

```text
Identify User-Controlled Input
          ↓
Submit Controlled Test Input
          ↓
Observe Application Behavior
          ↓
Examine the Resulting Page
          ↓
Determine Where Input Appears
          ↓
Understand the HTML/JavaScript Context
          ↓
Adapt Testing When Necessary
          ↓
Determine Whether Code Execution Is Possible
```

This room gave me a better understanding of what to look for instead of simply placing the same test input into every field.

---

# Interview Notes

### What is XSS?

Cross-Site Scripting is a web application vulnerability where attacker-controlled input is handled insecurely and results in script execution within a user's browser in the context of the vulnerable website.

### What is Reflected XSS?

Reflected XSS occurs when attacker-controlled input is sent to an application and immediately reflected within the application's response in an unsafe context.

### What is Stored XSS?

Stored XSS occurs when attacker-controlled input is stored by the application and later returned to users when affected content is viewed.

### What is Blind XSS?

Blind XSS occurs when attacker-controlled input is submitted but the tester cannot directly observe where or when the payload executes.

### What is DOM-Based XSS?

DOM-based XSS is a client-side vulnerability where JavaScript handles attacker-controlled data unsafely and modifies the DOM in a way that can cause script execution.

### Does reflected input automatically mean XSS exists?

No. Seeing controlled input reflected on a webpage does not automatically prove XSS. The tester must determine whether the input can reach an executable browser context.

### Why is JavaScript important for XSS?

JavaScript is important because XSS commonly involves causing attacker-controlled JavaScript to execute within another user's browser in the context of the vulnerable application.

### Why is viewing page source useful?

Viewing the page source can help determine where controlled input appears within the webpage and provide information about the context in which the input is being handled.

---

# Key Takeaway

The biggest takeaway from this room was gaining a better understanding of how XSS actually works.

A useful mental model is:

```text
Attacker-Controlled Input
          ↓
Application Handles Input Unsafely
          ↓
Input Reaches Browser
          ↓
Browser Interprets Input as Code
          ↓
JavaScript Executes
```

I also learned that identifying reflected input is only the beginning of XSS testing.

Understanding where the input appears and whether it can reach an executable browser context is what helps determine whether an actual XSS vulnerability exists.

---

# Skills Developed

- Cross-Site Scripting Fundamentals
- Reflected XSS Identification
- Stored XSS Identification
- Blind XSS Awareness
- DOM-Based XSS Awareness
- HTML Source Analysis
- JavaScript Execution Analysis
- User-Controlled Input Identification
- HTTP Request and Response Analysis
- Web Application Testing
- XSS Testing Methodology
- Browser-Side Security Concepts

---

# Screenshots

Useful screenshots for this room could include:

- Search box or form being tested
- Controlled input appearing within the application
- Page source showing where controlled input appears
- Successful proof-of-concept JavaScript execution
- Examples from different XSS exercises
- Stored input before and after it is viewed

Sensitive information, credentials, flags, and lab answers should be redacted before uploading screenshots to a public GitHub repository.

---

# Personal Reflection

## Biggest Lesson Learned

The biggest lesson I learned from this room was gaining a better understanding of how XSS works.

I learned how attacker-controlled input can be handled insecurely by a web application and potentially execute within a user's browser.

## Why HTML and JavaScript Matter

Understanding HTML and JavaScript will help me during future web penetration tests because it will make it easier to understand how a web application handles user-controlled input and identify areas where XSS vulnerabilities may exist.

Improving these skills will also help me better understand why different XSS testing approaches work in different contexts.

## Most Interesting Concept

Stored XSS interested me the most because the attacker-controlled input is stored by the application instead of only being immediately reflected.

I found it interesting that the stored input can potentially execute later when affected content is viewed.

## Future Penetration Tests

This room will help me during future web application penetration tests because I now have a better understanding of how to look for potential XSS vulnerabilities.

I learned to identify user-controlled input, observe how the application handles it, examine where the input appears within the page, and determine whether the input can reach an executable browser context.