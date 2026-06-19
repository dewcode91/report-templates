# Cross-Site Scripting (XSS) Vulnerability in Search Parameter

## Summary

A Cross-Site Scripting (XSS) vulnerability exists in the search parameter of [https://www.example.com/search?q=](https://www.example.com/search?q=). An attacker can inject malicious JavaScript via the `q` parameter, leading to arbitrary script execution in users' browsers.

## Steps to Reproduce

1. Navigate to:  
   `https://www.example.com/search?q=%27-alert(document.domain)-%27`
2. An alert pop-up will appear, demonstrating code execution.

## Impact

This vulnerability allows attackers to:
- Steal sensitive user information (e.g., session cookies)
- Hijack user accounts
- Perform actions as other users (impersonation)
- Conduct phishing attacks or deface the site

Such issues can result in reputational harm, legal liability, and loss of user trust.

## Recommendation

Sanitize and properly encode user-supplied input in the search parameter to prevent script injection.
