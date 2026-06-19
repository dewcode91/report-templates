# Unauthorized Access to Admin Panel via Client-Side Role Control

#### Description

The application determines user privileges at login and stores them in a user-controllable location (e.g., hidden field, cookie, or query string parameter). This allows attackers to easily elevate their privileges by modifying these values, granting themselves unauthorized admin access. For example:

- `https://insecure-website.com/login/home.jsp?admin=true`
- Cookie: `Admin=true`

The following HTTP request shows the insecure usage of an `Admin` cookie:

```
GET /admin HTTP/1.1
Host: ac961f1c1ef4adef80bd6a6c0000006c.web-security-academy.net
...
Cookie: session=DOOAJa8Mkf2EDu4mLoLImfnDaP5My8yS; Admin=false
...
```

#### Steps to Reproduce

1. Attempt to access `/admin` to confirm lack of access.
2. Log in via the standard user login page.
3. Intercept the login response (e.g., with Burp Suite) and observe the `Admin=false` cookie being set.
4. Modify the cookie to `Admin=true` and resend the request.
5. Access `/admin`—the user now has admin privileges.

#### Impact

This vulnerability enables any user to gain administrative access by simply changing the client-side value, potentially resulting in privilege escalation, unauthorized actions (e.g., deleting users), and full system compromise.

#### Recommendation

Implement server-side access control checks for all sensitive endpoints. Do not rely on user-modifiable data such as cookies or URL parameters for authorization decisions.
