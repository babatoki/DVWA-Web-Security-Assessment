# DVWA Web Application Security Assessment Report

## 1. Executive Summary

A controlled web application security assessment was performed against Damn Vulnerable Web Application (DVWA) in an isolated cybersecurity laboratory environment. The assessment was conducted from Kali Linux and focused on identifying common web application security weaknesses.

Testing identified several security issues, including PHP information disclosure, directory listing, SQL injection, reflected cross-site scripting (XSS), and session/logout security concerns.

The findings demonstrate how insecure application configurations and insufficient input and session controls can expose web applications to information disclosure, unauthorized database interaction, client-side attacks, and session-related risks.

## 2. Scope

### Target

- Damn Vulnerable Web Application (DVWA)
- Intentionally vulnerable laboratory application

### Testing Environment

- Kali Linux
- Virtualized laboratory environment
- Web browser
- Nmap
- cURL
- DVWA

### Authorization

Testing was performed against an intentionally vulnerable application within a controlled laboratory environment for cybersecurity education and authorized security testing.

## 3. Methodology

The assessment followed a structured web application testing process:

1. Reconnaissance
2. Web enumeration
3. Information disclosure assessment
4. Directory/resource enumeration
5. SQL injection testing
6. Reflected XSS testing
7. Session and logout testing
8. Evidence collection
9. Risk assessment
10. Remediation analysis

## 4. Findings Summary

| ID | Finding | Severity |
|---|---|---|
| WEB-01 | PHP Information Disclosure | Medium |
| WEB-02 | Directory Listing | Medium |
| WEB-03 | SQL Injection | High |
| WEB-04 | Reflected XSS | Medium |
| WEB-05 | Session/Logout Security Weakness | Medium |

## 5. Detailed Findings

### WEB-01 — PHP Information Disclosure

**Severity:** Medium

#### Description

PHP configuration information was accessible through the web application. Information disclosure can provide attackers with useful details about the application's runtime environment and server configuration.

#### Security Impact

Exposed configuration information can assist attackers during reconnaissance and help them identify technologies, versions, configuration settings, and potential attack paths.

#### Evidence

![PHP Information Disclosure](screenshots/enumeration/02-phpinfo.png)

#### Recommendation

Disable publicly accessible PHP configuration information in production environments. Remove or restrict diagnostic pages and ensure that configuration details are only accessible to authorized administrators.

---

### WEB-02 — Directory Listing

**Severity:** Medium

#### Description

Directory listing behavior was identified during web enumeration. This can expose application files and resources that were not intended to be directly browsable.

#### Security Impact

Exposed directories may reveal application structure, files, backups, configuration information, or other resources that can assist further attacks.

#### Evidence

![Directory Listing](screenshots/enumeration/03-directory-listing.png)

#### Recommendation

Disable directory indexing on production web servers unless it is explicitly required. Restrict access to sensitive directories and ensure that unnecessary files are removed from publicly accessible locations.

---

### WEB-03 — SQL Injection

**Severity:** High

#### Description

SQL injection testing was performed against the deliberately vulnerable DVWA application. The application demonstrated behavior consistent with insufficient protection of user-supplied database input.

#### Security Impact

SQL injection can allow attackers to manipulate database queries. Depending on database privileges and application architecture, successful exploitation may allow unauthorized data access, modification, or other database-level compromise.

#### Evidence

![SQL Injection](screenshots/findings/04-sql-injection.png)

#### Recommendation

Use parameterized queries and prepared statements. Validate input on the server side and apply least-privilege permissions to database accounts. Avoid constructing SQL queries directly from untrusted user input.

---

### WEB-04 — Reflected Cross-Site Scripting

**Severity:** Medium

#### Description

Reflected cross-site scripting testing was performed against the vulnerable application. User-controlled input was reflected in the application's response without sufficient output encoding.

#### Security Impact

Successful reflected XSS exploitation can allow malicious script content to execute in a victim's browser. Potential consequences include phishing, session-related attacks, unauthorized browser actions, and manipulation of displayed content.

#### Evidence

![Reflected XSS](screenshots/findings/05-reflected-xss.png)

#### Recommendation

Implement context-aware output encoding and appropriate input validation. Deploy a strong Content Security Policy where practical and avoid inserting untrusted input directly into HTML, JavaScript, or other executable contexts.

---

### WEB-05 — Session and Logout Security

**Severity:** Medium

#### Description

Session and logout behavior was assessed as part of the web application security review.

#### Security Impact

Weak session termination can increase the risk of unauthorized access if an attacker obtains a valid session identifier or gains access to a previously authenticated browser session.

#### Evidence

![Session Testing](screenshots/findings/06-session-logout.png)

#### Recommendation

Applications should invalidate server-side sessions during logout. Session identifiers should be regenerated after authentication, and cookies should use appropriate security attributes such as `HttpOnly`, `Secure`, and `SameSite`.

## 6. Risk Overview

The assessment identified one high-severity finding and four medium-severity findings.

The highest-priority issue was SQL injection because database-level attacks can potentially result in unauthorized access to sensitive information and manipulation of application data.

The medium-severity findings should also be addressed because information disclosure, XSS, directory exposure, and weak session controls can provide attackers with additional opportunities to compromise an application or its users.

## 7. Recommended Security Improvements

The following controls are recommended:

1. Use parameterized SQL queries and prepared statements.
2. Validate and securely handle user input.
3. Apply context-aware output encoding.
4. Disable unnecessary diagnostic and configuration pages.
5. Disable directory indexing on production systems.
6. Remove unnecessary files and resources from web-accessible directories.
7. Implement secure session invalidation during logout.
8. Regenerate session identifiers after authentication.
9. Configure secure cookie attributes.
10. Apply least-privilege permissions to application and database accounts.
11. Keep web applications, frameworks, and supporting software patched.
12. Perform recurring vulnerability assessments and penetration tests.

## 8. Conclusion

The assessment demonstrated several common web application security weaknesses in the intentionally vulnerable DVWA environment. The findings illustrate the importance of secure input handling, proper output encoding, secure session management, restricted information disclosure, and appropriate web server configuration.

The assessment also demonstrates a practical penetration-testing workflow involving reconnaissance, enumeration, vulnerability testing, evidence collection, risk classification, and remediation recommendations.

## 9. Ethical Use

All testing documented in this report was performed against an intentionally vulnerable application within an authorized and controlled laboratory environment.

The techniques described should only be used against systems for which explicit authorization has been provided.
