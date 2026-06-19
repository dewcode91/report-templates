# Open Redirect Leading to Cross-Site Scripting (XSS)

#### Description
The application allows users to access external resources via a redirect functionality. The `destUrl` parameter in URLs such as `https://insecure-website.com/resources/course/redirect?destUrl=payload` is not properly validated or restricted, resulting in an open redirect vulnerability. Attackers can leverage this to redirect users to any external site or even inject JavaScript payloads, leading to potential XSS attacks.

#### Steps to Reproduce

1. Log in to your account.
2. Navigate to **Resources > Online Courses**.
3. Select any course and click on **View Course**.
4. Before being redirected to the course page, copy the URL from the address bar.
5. Replace the `destUrl` value with a JavaScript payload, e.g., `javascript:alert(document.cookie)`.
6. Visiting this crafted URL will execute the script in the user's browser.

#### Impact
Exploitation of this vulnerability can result in:

- Execution of arbitrary JavaScript in the victim's browser (XSS).
- Theft of sensitive user information such as session cookies.
- Phishing or social engineering attacks redirecting users to malicious sites.
- Potential for unauthorized access to user accounts.

#### Recommendation
Validate and restrict the `destUrl` parameter to prevent redirection to untrusted sites and block JavaScript execution. Consider implementing a whitelist of allowed domains and disallow the use of schemes like `javascript:`.
