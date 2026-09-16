# Phishing Email Investigation — SOC Analysis

## Project Overview
This project involved the investigation of a suspected phishing email 
targeting employees of a simulated healthcare organization. The 
investigation focused on identifying phishing indicators, analyzing 
email authentication results, examining the embedded URL, and 
determining appropriate remediation measures.

This was completed as a group SOC analysis project (March 2026, Group 1).

## Investigation Objectives
- Identify indicators of phishing and social engineering
- Analyze email headers and sender authentication
- Examine the embedded URL for malicious or suspicious activity
- Use security analysis tools to validate findings
- Recommend appropriate remediation and prevention measures

## Attack Scenario
The suspicious email impersonated the organization's security team and 
created a sense of urgency by claiming unusual account activity had 
been detected. The recipient was instructed to verify their account 
through an embedded link, with a threat of account suspension.

Suspicious characteristics identified:
- Urgent and threatening language
- An account-verification request
- A suspicious hyperlink
- Failed email authentication checks
- A sending IP inconsistent with normal public email infrastructure
- A link redirecting to a domain unrelated to the organization

## Analysis Performed

**1. Initial Email Review**
Reviewed for common social-engineering indicators: urgency, fear, 
impersonation, and a suspicious verification link.

**2. Email Header Analysis**
Examined headers using MXToolbox and Outlook's raw header view. 
Identified authentication failures across SPF, DKIM, and DMARC, plus 
sender/Message-ID inconsistencies.

**3. URL Analysis**
Analyzed the embedded URL using VirusTotal — multiple vendors flagged 
it as suspicious/phishing-associated. Opened it in a controlled 
Browserling environment to safely observe redirect behavior without 
exposing a live system.

## Tools Used
| Tool | Purpose |
|------|---------|
| Outlook | Review suspicious email and extract headers |
| MXToolbox | Analyze email headers and authentication |
| VirusTotal | Analyze the embedded URL |
| Browserling | Safely observe URL behavior and redirects |

## Indicators of Compromise
- Failed SPF, DKIM, and DMARC checks
- Suspicious verification URL
- Redirect to an unrelated domain
- Social-engineering language designed to create urgency and fear

## Recommended Remediation
- Enforce stronger email authentication (DMARC enforcement policy)
- Require secondary verification for urgent account-related requests
- Provide regular phishing-awareness training
- Enable MFA for critical accounts
- Provide a clear process for reporting suspicious emails
- Use sandboxing for suspicious links/attachments
- Block confirmed malicious domains after validation

## Key Takeaways
This investigation demonstrated how SOC analysts combine email 
analysis, authentication checks, threat intelligence, and URL 
analysis to investigate a phishing attack — and how technical 
controls must be paired with user awareness, since phishing relies 
heavily on social engineering.

## My Contribution
As a member of Group 1, I participated in the investigation and 
analysis of the phishing email, including review of phishing 
indicators, email authentication data, URL analysis, and security 
recommendations.

## Project Evidence
Screenshots and supporting evidence are included in the `screenshots/` 
folder.

**Note:** This was a simulated/training SOC investigation. Sensitive 
information has been sanitized for public publication.
