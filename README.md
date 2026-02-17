Web Security Research Lab

Documentation of hands-on vulnerability analysis and remediation.

Vulnerabilities Analyzed
* **SQL Injection (SQLi):** Demonstrated authentication bypass and data extraction.
* **Remote Code Execution (RCE):** Exploited unsafe system calls to gain shell access.
* **Cross-Site Scripting (XSS):** Analyzed DOM-based vulnerabilities and script injection.

Remediation Strategies
* Implementation of **Parameterized Queries** for database security.
* Migrated to `subprocess` with `shell=False` for OS command safety.
* Applied context-aware **Output Encoding** for XSS prevention.

---
*Developed in a ParrotOS Lab Environment.*
