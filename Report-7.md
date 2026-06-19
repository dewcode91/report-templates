# Blind SSRF via "Import Calendar from URL" Feature

## Summary
The "Import Calendar from URL" functionality in the calendar application is vulnerable to blind Server-Side Request Forgery (SSRF). This allows attackers to make the server initiate requests to internal network resources or conduct port scanning, which may lead to sensitive information disclosure or further compromise of internal systems.

## Vulnerability Details

While reviewing the calendar app, I discovered that the feature for importing calendars from external URLs can be exploited for SSRF:

- When attempting to import a calendar from `http://127.0.0.1/`, the server correctly blocks the request and returns `unsupported_url`.
- However, specifying a local address with an explicit port, such as `http://127.0.0.1:22`, results in a successful (albeit blank) calendar import. Ports 22, 25, and 873 responded during my scan across ports 1-1000.
- This behavior enables attackers to probe internal network ports and potentially interact with services that should not be exposed, risking data exfiltration or further attacks.

## Steps to Reproduce

1. Log in to `https://calendar.example.com`.
2. Click the import icon next to "Calendars" and select "From a URL".
3. Enter a URL like `http://127.0.0.1:22` and observe the system’s response.

## Impact

By exploiting this vulnerability, attackers can:

- **Conduct Internal Port Scans:** The server can be used to scan internal IPs and ports, identifying potential internal services and weaknesses.
- **Access Restricted Resources:** Attackers may reach internal services or files not accessible externally, risking data leakage or further exploitation.
- **Enable Further Attacks:** Gaining information about internal network structure and open ports can assist in lateral movement or other attack vectors.

## Recommendation

- Implement strict allow-lists for external URLs and disallow any access to internal IP ranges and reserved addresses, regardless of port.
- Sanitize and validate all input URLs to prevent SSRF attacks.
- Monitor and alert on suspicious import attempts, especially those targeting private network ranges or unusual ports.
