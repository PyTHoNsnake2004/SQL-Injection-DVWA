# SQL Injection on DVWA (Low Security)

## Objective
Demonstrate a SQL Injection vulnerability in DVWA with its security set to low.

## Setup
1. DVWA was hosted on [Metasploitable 2 VM/IP: 192.168.0.103].
2. Security level was set to "Low" in the DVWA Security settings.

## The Vulnerability
The application takes user input (User ID) and directly uses it in an SQL query without any sanitization, leading to SQL Injection.

## Exploitation
**Payload Used:** `' OR '1'='1`
- This payload manipulates the SQL query to always return TRUE, bypassing intended logic.
- The original query: `SELECT first_name, last_name FROM users WHERE user_id = '$id';`
- becomes: `SELECT first_name, last_name FROM users WHERE user_id = '' OR '1'='1';`

**Advanced Payload:** `' UNION SELECT user, password FROM users#`
- This payload attempts to extract usernames and password hashes from the database.

## Impact
- Authentication Bypass: An attacker can log in without a valid password.
- Information Disclosure: An attacker can extract sensitive data from the database (like user credentials).
- Data Manipulation: An attacker can modify or delete database data.

## Prevention
- Use Prepared Statements (Parameterized Queries).
- Validate and sanitize all user input.
- Implement the principle of least privilege on the database user.
- Keep software updated.

## Screenshots
- See attached images for proof of concept.
