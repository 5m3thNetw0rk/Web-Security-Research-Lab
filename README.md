Web Security Research Lab

This repository documents hands-on analysis, exploitation, and remediation of critical web vulnerabilities. The goal of this project is to demonstrate a "Full-Spectrum" understanding of security—from identifying a flaw to implementing a production-ready fix.

I utilized a **ParrotOS** lab environment to build a controlled, vulnerable Flask application. Each vulnerability was tested using manual exploitation techniques and industry-standard tools before being patched with secure coding practices.

1. SQL Injection (SQLi)
* **Vulnerability:** Unsanitized input in authentication queries.
* **Remediation:** Migrated from raw string formatting to **Parameterized Queries** to prevent database manipulation.

2. Remote Code Execution (RCE)
* **Vulnerability:** Unsafe use of `os.system()` allowing command injection.
* **Remediation:** Replaced shell calls with the `subprocess` module using `shell=False` to isolate commands from the system shell.

3. Cross-Site Scripting (XSS)
* **Vulnerability:** Reflected input without context-aware encoding.
* **Remediation:** Implemented **Jinja2 Auto-escaping** and manual input sanitization to prevent script execution in the browser.

Tech Stack
* **OS:** Parrot Security OS
* **Language:** Python 3.x
* **Framework:** Flask
* **Database:** SQLite3
