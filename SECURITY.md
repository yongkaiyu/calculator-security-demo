# Security Scanning

## Overview
This repository uses three types of security scanning:

### SAST (Static Analysis with CodeQL)
- Scans source code for vulnerabilities
- Runs on push to main branch
- Checks for: [SQL injection, command injection, path traversal, input validation, sanitization issues, hardcoded secrets or sensitive data exposure, unsafe API, file operations]
- Artifacts: See GitHub Security tab

### SCA (Dependency Check)
- Scans Python packages for known CVEs
- Runs on push to main branch
- Checks for: [outdated or vulnerable package versions, known CVEs reported for dependencies, retried or deprecated libraries]
- Artifacts: sca-reports

### DAST (Live Application with ZAP)
- Tests running application for vulnerabilities
- Runs on push to main branch
- Checks for: [missing security headers, runtime configuration issues, exposed endpoints, response anomalies, browser security misconfigurations]
- Artifacts: zap-baseline-reports, zap-fullscan-reports

## Understanding Results
[ DAST Results (ZAP Baseline)
- Total URLs scanned: 3
- PASS: 61 checks
- WARN-NEW: 9 warnings
- FAIL-NEW: 0 failures

Warning Summary
[WARN-NEW: Missing Anti-clickjacking Header [10020] x 1 
	http://localhost:5000 (200 OK)
WARN-NEW: X-Content-Type-Options Header Missing [10021] x 1 
	http://localhost:5000 (200 OK)
WARN-NEW: Server Leaks Version Information via "Server" HTTP Response Header Field [10036] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)
WARN-NEW: Content Security Policy (CSP) Header Not Set [10038] x 2 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
WARN-NEW: Storable and Cacheable Content [10049] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)
WARN-NEW: Permissions Policy Header Not Set [10063] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)
WARN-NEW: Modern Web Application [10109] x 1 
	http://localhost:5000 (200 OK)
WARN-NEW: Insufficient Site Isolation Against Spectre Vulnerability [90004] x 3 
	http://localhost:5000 (200 OK)
	http://localhost:5000 (200 OK)
	http://localhost:5000 (200 OK)
WARN-NEW: Sec-Fetch-Dest Header is Missing [90005] x 12 
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)
	http://localhost:5000/sitemap.xml (404 Not Found)
	http://localhost:5000 (200 OK)
	http://localhost:5000/robots.txt (404 Not Found)]
]

## Reporting Vulnerabilities
https://github.com/yongkaiyu/calculator-security-demo/actions
