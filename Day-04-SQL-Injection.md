# Day 04 - SQL Injection

## What It Is
SQL Injection is a web attack where malicious SQL code is inserted into an input field to manipulate the database query running behind the scenes. Instead of the app processing your input as data, it gets executed as a database command. It's one of the most common and damaging vulnerabilities in web applications.

## How It Works
Web apps take user input and use it to build database queries. The problem is when that input isn't properly sanitized, an attacker can break out of the intended query and inject their own SQL logic.

Classic example - a login form:
```sql
-- Normal query the app builds
SELECT * FROM users WHERE username='john' AND password='1234';

-- Attacker enters:  ' OR '1'='1  in the username field
SELECT * FROM users WHERE username='' OR '1'='1' AND password='';
```

Since `'1'='1'` is always true, the query returns all users and the attacker gets in without a valid password. From here depending on the database and permissions the attacker can read tables, dump credentials, modify data, or even execute OS commands.

There are three main types:
- In-band SQLi: results come back directly in the app response
- Blind SQLi: no visible output, attacker infers data from true/false responses
- Out-of-band SQLi: data is sent to an external server the attacker controls
