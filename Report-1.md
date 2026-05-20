# Unrestricted Admin Features Exposed via `robots.txt`

## Description
This issue is a **vertical privilege escalation** caused by exposing an administrative path in `robots.txt`. Attackers can enumerate `robots.txt` or brute-force common admin paths to discover and access sensitive functionality.

Example:
- Admin path: `https://insecure-website.com/admin`
- `robots.txt`: `https://insecure-website.com/robots.txt`

If the admin path is listed, unauthorized users can directly access privileged interfaces.

## Steps to Reproduce
1. Visit `https://<target>/robots.txt`.
2. Identify any `Disallow` entries referencing admin paths.
3. Replace `/robots.txt` with the disclosed admin path (e.g., `/admin`).
4. Confirm access to privileged functionality (e.g., user deletion).

## Impact
Unauthorized users can access administrative features, enabling:
- Data modification or deletion
- Configuration changes
- Account management (including privilege escalation)

This threatens the application’s confidentiality, integrity, and availability.

## Recommendation
- Remove sensitive paths from `robots.txt`.
- Enforce **server-side access control** on all admin endpoints.
- Add monitoring for admin-path enumeration.
