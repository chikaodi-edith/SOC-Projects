
# Security Log Analysis

## Project Overview

This project involved a manual analysis of a security log dataset containing **1,000 log entries** recorded on April 1, 2026.

The objective was to identify suspicious authentication activity, detect potential threats, investigate attack patterns, and provide recommendations for improving the organization's security posture.

The analysis was performed individually using **Microsoft Excel**, with filters, sorting, and pivot tables used to investigate the dataset.

> **Note:** This project was completed as part of a cybersecurity analysis assignment using a provided security log dataset. The dataset's original organizational source was not specified in the assignment materials.

## Analysis Objectives

- Identify suspicious authentication activity.
- Investigate failed and successful login attempts.
- Detect brute-force attacks.
- Identify password-spraying patterns.
- Investigate possible username enumeration.
- Analyze suspicious source IP addresses.
- Examine account lockouts and special-privilege events.
- Recommend appropriate security controls and remediation measures.

## Dataset Overview

| Category | Details |
|---|---|
| Total Log Entries | 1,000 |
| Date | April 1, 2026 |
| Analysis Tool | Microsoft Excel |
| Unique Event IDs | 4624, 4625, 4634, 4672, 4688, 4740 |
| Unique Hostnames | APP02, DC01, FW01, MAIL01, WEB01, WS100, WS101 |
| Source IPs | 59 |
| Network Range | 10.0.1.x |

## Key Findings

### 1. Failed Login Activity

Multiple user accounts recorded high numbers of failed authentication attempts.

The most frequently targeted accounts included:

- `svc_backup` — 133 failed attempts
- `charlie` — 131
- `bob` — 130
- `alice` — 126
- `david` — 126
- `guest` — 125
- `eve` — 119
- `admin` — 109

The concentration of failed attempts across multiple accounts indicated persistent authentication attacks.

### 2. Brute-Force Activity

The `svc_backup` account showed a pattern of multiple failed login attempts followed by a successful authentication.

This pattern was identified as evidence of a **successful brute-force attack** within the training scenario.

The `guest` account also showed a similar pattern involving failed attempts followed by a successful login at 08:14.

### 3. Password Spraying

The analysis identified authentication attempts distributed across multiple user accounts and source IP addresses.

The relatively even distribution of failed attempts across the eight accounts was consistent with a **password-spraying pattern**, where attackers attempt credentials across multiple accounts rather than repeatedly targeting only one account.

### 4. Username Enumeration

All eight analyzed accounts were targeted with substantial numbers of failed authentication attempts.

The distribution of activity across accounts was consistent with systematic testing of usernames or previously obtained account information.

### 5. Suspicious Source IP Activity

Several internal IP addresses recorded high numbers of authentication attempts.

The most notable addresses included:

- `10.0.1.10`
- `10.0.1.21`
- `10.0.1.55`

These addresses required further investigation to determine whether the activity originated from legitimate internal systems or potentially compromised hosts.

### 6. Special Privilege Events

Event ID **4672 (Special Privileges Assigned to New Logon)** was observed during the investigation.

The `svc_backup` and `guest` accounts showed particularly notable activity.

These events were reviewed as part of the investigation because unexpected special-privilege assignments can indicate potentially risky account activity.

## Tools Used

**Microsoft Excel**

Used for:

- Filtering log entries
- Sorting authentication events
- Creating pivot tables
- Counting failed logins
- Identifying account lockouts
- Investigating source IP activity
- Reviewing event patterns

## Security Events Analyzed

The investigation included the following Windows security event IDs:

- **4624** — Successful logon
- **4625** — Failed logon
- **4634** — Logoff
- **4672** — Special privileges assigned to new logon
- **4688** — New process created
- **4740** — User account locked out

## Recommendations

Based on the findings, the following security measures were recommended:

1. Implement appropriate account lockout controls to reduce brute-force attempts.
2. Disable or restrict unnecessary default and guest accounts.
3. Review the permissions and usage of service accounts such as `svc_backup`.
4. Enable MFA, particularly for privileged and sensitive accounts.
5. Configure SIEM or security monitoring alerts for repeated authentication failures.
6. Alert on successful logins following repeated failed attempts.
7. Monitor unusual Event ID 4672 activity.
8. Investigate internal systems associated with repeated suspicious authentication attempts.
9. Apply appropriate network controls after confirming unauthorized activity.
10. Continue monitoring authentication logs for recurring attack patterns.

## Skills Demonstrated

- Security log analysis
- Authentication event analysis
- Threat detection
- Brute-force detection
- Password-spraying analysis
- Username enumeration analysis
- Account lockout investigation
- Source IP investigation
- Windows Event ID analysis
- Microsoft Excel
- Security incident investigation

## Project Evidence

The `Report` folder contains the detailed technical report.

The `Screenshots` folder contains supporting evidence from the analysis process.

## Key Takeaway

This project demonstrated how security analysts can use authentication logs to identify suspicious patterns and investigate potential threats.

By combining event IDs, usernames, timestamps, source IP addresses, and authentication outcomes, it is possible to identify patterns associated with brute-force attacks, password spraying, account compromise, and other suspicious activity.
