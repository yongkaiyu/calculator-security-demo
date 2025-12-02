# Security Scan Analysis - [2/12/25]

## DAST Results (ZAP Baseline)
- Total URLs scanned: 3
- PASS: 61 checks
- WARN-NEW: 9 warnings
- FAIL-NEW: 0 failures

### Warning Summary
[
WARN-NEW: Missing Anti-clickjacking Header [10020] x 1 
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

## SCA Results (Dependency Check)
- High severity: 0
- Medium severity: 0
- Low severity: 0

### Vulnerable Packages
None found

## SAST Results (CodeQL)
- Total issues: 1
- By type: [security]

## Recommendations
Switching to a production server should be prioritized







Table Mapping

| Issue Code | Warning Name                            | Risk Level     | Affected URL(s)                                                                 | Prevented Attack                                                                                                          |
| ---------- | --------------------------------------- | -------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **10020**  | Missing Anti-clickjacking Header        | **Medium**     | `http://localhost:5000`                                                         | Prevents **clickjacking attacks** where attackers trick users into clicking hidden UI elements.                           |
| **10021**  | X-Content-Type-Options Header Missing   | **Low/Medium** | `http://localhost:5000`                                                         | Prevents **MIME-sniffing**, where browsers incorrectly interpret file types and may execute malicious content.            |
| **10036**  | Server Leaks Version Information        | **Low**        | `http://localhost:5000`<br>`/robots.txt`<br>`/sitemap.xml`                      | Prevents **information disclosure**, which attackers use to target known vulnerabilities in specific server versions.     |
| **10038**  | Content Security Policy (CSP) Not Set   | **High**       | `http://localhost:5000`<br>`/robots.txt`                                        | Prevents **XSS, code injection, clickjacking, and malicious script execution**. CSP is one of the strongest web defenses. |
| **10049**  | Storable and Cacheable Content          | **Low**        | `http://localhost:5000`<br>`/robots.txt`<br>`/sitemap.xml`                      | Prevents **sensitive data exposure via caching** in browsers or intermediate proxies.                                     |
| **10063**  | Permissions-Policy Header Not Set       | **Low**        | `http://localhost:5000`<br>`/robots.txt`<br>`/sitemap.xml`                      | Prevents unauthorized use of **browser features** such as camera, microphone, geolocation, fullscreen, etc.               |
| **10109**  | Modern Web Application                  | **Info/Low**   | `http://localhost:5000`                                                         | Indicates missing **modern security best practices** (headers, protections). Not a direct vulnerability.                  |
| **90004**  | Insufficient Site Isolation for Spectre | **Low**        | `http://localhost:5000` (x3)                                                    | Helps mitigate **Spectre CPU side-channel attacks**, where data may be read across site boundaries.                       |
| **90005**  | Sec-Fetch-Dest Header Missing           | **Low**        | `http://localhost:5000`<br>`/robots.txt`<br>`/sitemap.xml` (multiple instances) | Prevents **request context confusion** and improves defenses against CSRF-like request manipulation.                      |

| Tool                       | Unique Findings                                                                                | Notes                                                                                 |
| -------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **SAST (CodeQL)**          | - Code patterns and logic errors<br>- Data flow vulnerabilities                                | Detects **issues in source code** that cannot be seen at runtime.                     |
| **DAST (ZAP)**             | - Missing security headers<br>- Runtime configuration issues<br>- API endpoint vulnerabilities | Detects **runtime misconfigurations** and exposure of endpoints.                      |
| **SCA (Dependency-Check)** | - Outdated package versions<br>- Known CVEs in dependencies                                    | Detects **vulnerabilities in third-party libraries**, not visible in code or runtime. |

| Finding Type                 | Tools That Can Detect | Notes                                                                                                   |
| ---------------------------- | --------------------- | ------------------------------------------------------------------------------------------------------- |
| Input validation / injection | SAST, partially DAST  | SAST identifies unsafe code paths; DAST triggers vulnerabilities via HTTP requests.                     |
| Hardcoded secrets            | SAST, partially SCA   | SAST detects hardcoded keys; SCA can flag vulnerable libraries containing secrets.                      |
| Missing security headers     | DAST, optionally SAST | Only visible during runtime; SAST may only detect via annotations or framework-specific rules.          |
| All three tools              | Rare                  | Tools focus on different layers (code, runtime, dependencies), so overlap across all three is uncommon. |
