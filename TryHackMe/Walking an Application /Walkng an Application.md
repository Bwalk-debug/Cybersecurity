 # Walking an Application

**Platform:** TryHackMe  
**Learning Path:** Jr Penetration Tester  
**Room:** Walking an Application  
**Date Completed:** August 16, 2026  
**Difficulty:** Easy  
**Room Type:** Reading + Hands-on (Browser Developer Tools)

---

# Objective

The objective of this room was to learn how to inspect a web application, understand its human-readable source code, identify information that could reveal security weaknesses, and use browser developer tools to better understand how a website functions.

---

# Why Walking an Application Matters

Before attempting to exploit a web application, a penetration tester must first understand how it works. Walking an application involves examining the website's structure, source code, developer tools, and client-side resources to identify potential attack surfaces before testing for vulnerabilities.

---

# Web Application Concepts

## HTML

HTML (HyperText Markup Language) is the standard markup language used to structure a web page. It defines elements such as headings, forms, buttons, links, images, and other content displayed in the browser.

---

## View Page Source

View Page Source displays the original HTML sent by the web server.

A penetration tester may discover:

- Developer comments
- Hidden directories
- JavaScript files
- Internal URLs
- References to hidden resources

---

## Inspect Element (Developer Tools)

Inspect Element displays the live Document Object Model (DOM) after the page has loaded.

Developer Tools allow a penetration tester to:

- Inspect HTML elements
- Modify HTML and CSS locally
- Debug JavaScript
- Analyze network requests
- View stored cookies and local storage

Any changes made using Developer Tools affect only the local browser session and do not modify the actual website.

---

## HTTP and HTTPS

### HTTP

- Protocol: HTTP
- Default Port: 80
- Encryption: No

### HTTPS

- Protocol: HTTPS
- Default Port: 443
- Encryption: TLS

HTTPS protects data exchanged between the client and the web server by encrypting network traffic.

---

## Client vs Server

### Client

The web browser sends HTTP or HTTPS requests to the server and displays the returned content.

### Server

The web server processes requests, generates responses, and sends HTML, CSS, JavaScript, and other resources back to the client.

---

# Web Application Reconnaissance

When inspecting a web application, a penetration tester should look for:

- Hidden comments
- Internal links
- JavaScript files
- Hidden form fields
- API endpoints
- Backup files
- Developer notes
- Authentication pages
- Client-side validation

---

# Techniques Learned

## View Page Source

### Purpose

Displays the original HTML returned by the web server.

### Why a Penetration Tester Uses It

Useful for discovering information that may not be visible through the normal user interface, including comments, hidden references, and resources for further enumeration.

### Limitations

Does not display changes made dynamically by JavaScript after the page loads.

---

## Inspect Element

### Purpose

Displays the live HTML, CSS, and JavaScript running in the browser.

### Why a Penetration Tester Uses It

Useful for understanding how the application behaves, testing client-side changes, and identifying additional information about page elements.

### Limitations

Changes only affect the local browser session and do not modify the server.

---

# What I Learned

This room taught me that web application reconnaissance is just as important as network reconnaissance. Understanding the structure of a web application before attempting exploitation helps identify hidden resources, developer mistakes, and additional attack surfaces.

---

# Real-World Application

During a web application penetration test, inspecting the source code and browser developer tools can reveal information that is not immediately visible to users. This information can guide further enumeration and help identify potential vulnerabilities before attempting exploitation.

---

# Interview Notes

## What is HTML?

HTML (HyperText Markup Language) is the standard markup language used to structure web pages and define the content displayed by a browser.

---

## What is the difference between View Page Source and Inspect Element?

View Page Source displays the original HTML returned by the server, while Inspect Element displays the live DOM after JavaScript has modified the page.

---

## Why inspect a website's source code?

Inspecting source code can reveal hidden comments, references to directories, JavaScript files, API endpoints, and other information that may assist during reconnaissance.

---

## Why understand the application before exploitation?

Understanding how a web application works allows a penetration tester to identify attack surfaces before testing. This reduces unnecessary noise and leads to more focused, efficient security testing.

---

# Key Takeaway

Successful web application penetration testing begins with reconnaissance. Understanding how an application is built and identifying hidden information within its source code allows a penetration tester to develop a more effective and targeted testing strategy.

---

# Skills Developed

- Web Application Reconnaissance
- HTML Fundamentals
- View Page Source
- Browser Developer Tools
- Inspect Element
- Client-Side Analysis
- Information Gathering
- Web Enumeration

---

# Screenshots

This room involved using View Page Source and browser Developer Tools to inspect web applications. Screenshots were optional because the primary focus was understanding how to analyze source code and identify potential attack surfaces rather than collecting evidence from an exploited target.

---

# Personal Reflection

The biggest lesson I learned from this room is that viewing a web application's source code can reveal valuable information that is not immediately visible to users. Hidden comments, references to directories, JavaScript files, and other exposed information can provide clues that lead to vulnerabilities.

I also learned that understanding how an application works before attempting exploitation is essential. Proper reconnaissance reduces unnecessary noise and allows a penetration tester to focus on meaningful attack surfaces instead of guessing.

Viewing Page Source interested me the most because it allows me to inspect the original HTML returned by the server and identify information that may lead to additional enumeration.

This room will help me during future web application penetration tests because it introduced reconnaissance techniques that help identify potential vulnerabilities before exploitation begins.