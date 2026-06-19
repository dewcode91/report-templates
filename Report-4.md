# Broken Access Control Allows Unauthorized Admin Actions

## Description

Some applications control access by restricting specific URLs and HTTP methods based on user roles (e.g., denying `POST /admin/deleteUser` for non-admins). However, these defenses can be bypassed if the app or its platform honors non-standard HTTP headers—like `X-Original-URL` or `X-Rewrite-URL`—used to override the requested URL.

If an application enforces access rules only at a front-end layer but allows the effective URL to be overridden by these headers, attackers can access admin endpoints with crafted requests:

```
POST / HTTP/1.1
X-Original-URL: /admin/deleteUser
...
```

Alternatively, an attacker could exploit the vulnerability as follows:

```
GET /delete?username=carlos HTTP/1.1
Host: [target]
X-Original-URL: /admin
...
Cookie: session=[attacker-session-token]
```

This effectively bypasses URL-based access controls by tricking the backend into processing an unauthorized request.

## Steps to Reproduce

1. Attempt to access `/admin` as a non-admin user—access should be denied.
2. Send the request to an intercepting proxy (e.g., Burp Repeater).
3. Change the request line to `/` and add the header `X-Original-URL: /admin`.
4. Observe successful access to the admin page.
5. To perform actions (e.g., deleting a user), add parameters to the query string and adjust `X-Original-URL:` (e.g., `X-Original-URL: /admin/deleteUser` and `?username=carlos`).

## Impact

This vulnerability allows unauthorized users to perform critical admin actions, such as deleting users or changing configurations. Attackers could compromise data, disrupt service, or take full control of the application.
