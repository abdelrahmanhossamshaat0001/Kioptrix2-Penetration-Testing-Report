# Kioptrix Level 2 — Penetration Testing Report

An evidence-led, black-box penetration test of **Kioptrix Level 2**, conducted in an isolated and authorized VirtualBox laboratory.

The assessment demonstrates a complete compromise chain from an unauthenticated web user to full root access:

```text
SQL Injection → Authentication Bypass → OS Command Injection
→ Bash Shell as apache → CVE-2009-2698 → Root
```

> **Ethical-use notice:** Kioptrix is an intentionally vulnerable training machine. All testing was performed in a private educational lab. Do not test systems without explicit authorization.

## Engagement Overview

| Item | Details |
|---|---|
| Target | Kioptrix Level 2 — `192.168.56.104` |
| Attacker | Kali Linux — `192.168.56.102` |
| Assessment type | Black-box network and web application penetration test |
| Environment | Isolated VirtualBox host-only laboratory |
| Assessment date | 26 August 2026 |
| Final result | Full root compromise confirmed |
| Report author | AbdElrahman Hossam Shaat |

## Attack Chain

1. **Discovery** — Seven open ports were recorded on the target.
2. **Web enumeration** — A Remote System Administration login was identified.
3. **Authentication bypass** — SQL injection bypassed the login without valid credentials.
4. **Command execution** — The administrative ping function was vulnerable to operating-system command injection.
5. **Initial shell** — Bash command execution was obtained as `apache` (UID/GID 48).
6. **Post-exploitation** — A local exploit was transferred to the writable `/tmp` directory.
7. **Privilege escalation** — The Linux 2.6.9 kernel was exploited using CVE-2009-2698.
8. **Root confirmation** — Access was elevated to `root`, and the root mail spool was read.

## Recorded Lab Results

| # | Question / Field | Result |
|---|---|---|
| 1 | Open ports | 7 |
| 2 | Authentication bypass | SQL injection |
| 3 | Command execution | OS command injection |
| 4 | Shell type | Bash |
| 5 | Compromised user | `apache` |
| 6 | Kernel version | `2.6.9` |
| 7 | Linux distribution | CentOS |
| 8 | Distribution version | `4.5` |
| 9 | Privilege escalation | CVE-2009-2698 |
| 10 | GCC version | `3.4.6` |
| 11 | Writable exploit path | `/tmp` |
| 12 | Escalated user | `root` |
| 13 | Mail subject | `Postmaster notify: see transcript for details` |

## Findings

| ID | Finding | Severity |
|---|---|---|
| F-01 | SQL Injection Authentication Bypass | High |
| F-02 | Operating-System Command Injection | Critical |
| F-03 | Local Privilege Escalation via CVE-2009-2698 | High |
| F-04 | Unsupported Legacy Operating System and Components | Medium |

## Tools and Techniques

- Kali Linux
- Nmap
- Web application enumeration
- Manual SQL injection validation
- OS command injection
- Bash
- Python HTTP server
- Linux local privilege escalation

## Key Recommendations

- Replace dynamic SQL with parameterized queries and prepared statements.
- Remove shell-backed diagnostic functions and use safe library APIs.
- Apply strict allow-list validation to administrative network utilities.
- Rebuild the host using a supported Linux distribution and patched kernel.
- Run web applications under least privilege and restrict writable/execute paths.
- Add centralized logging and alerts for web-server child processes and privilege transitions.

## Deliverable

- [Kioptrix Level 2 Penetration Testing Report](./Kioptrix_Level_2_Penetration_Testing_Report.pdf) — 21-page report containing methodology, all seven supplied screenshots, the complete thirteen-item result register, findings, impact, and remediation.

## Evidence Note

The original lab submission preserved seven screenshots. Where a result had no dedicated screenshot, the report labels it as a **recorded result** rather than presenting fabricated visual evidence.

## Disclaimer

All credentials, IP addresses, vulnerabilities, and exploitation results relate exclusively to an intentionally vulnerable educational machine in an isolated lab.
