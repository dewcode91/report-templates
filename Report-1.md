# IDOR on `/api/v1/users/{id}/profile` allows unauthorized access to user PII

## Description

The `/api/v1/users/{id}/profile` endpoint fails to verify that the authenticated user matches the requested `{id}` parameter. By changing the user ID to another user's ID, an attacker can read that user's full profile, including name, email, phone number, and home address.

## Proof of Concept

```
GET /api/v1/users/1337/profile HTTP/2
Host: app.example.com
Authorization: Bearer eyJ...
Content-Type: application/json

---

HTTP/2 200 OK

{
  "id": 1337,
  "name": "Integriti",
  "email": "hunter2@example.com",
  "phone": "+1-555-5555",
  "address": "1337 Hackers Ave"
}
```

## Steps to Reproduce

1. Log in as user A (attacker) at app.example.com/login.
2. Navigate to your own profile and intercept the request to `/api/v1/users/{your_id}/profile`.
3. Change the user ID in the path to another user's ID (e.g., 1337).
4. Observe the full profile data of user 1337 in the response.

## Impact

Any authenticated user can read the full personal profile (name, email, phone, home address) of any other user on the platform by iterating over user IDs.
