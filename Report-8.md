# Information Disclosure: Django Debug Mode Enabled

## Description
The website `https://stage.example.com/` is operating with Django's debug mode enabled (`DEBUG = True`). When enabled, Django displays detailed error tracebacks with extensive environment metadata, including sensitive settings, upon encountering exceptions.

## Steps to Reproduce
1. Visit: https://stage.example.com/NON_EXISTING_PATH/
2. Observe the detailed debug information displayed in the error page.

## Impact
Debug mode exposes internal details such as configuration files, API keys, database credentials, and server directories. A malicious actor could exploit this information to compromise the system’s security.

## CVSS Score
[CVSS v3.0: 5.3 (Medium)](https://www.first.org/cvss/calculator/3.0#CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N)

## Recommendation
Disable Django debug mode (`DEBUG = False`) in all production and staging environments to prevent information leakage. Ensure sensitive settings are never exposed publicly.
