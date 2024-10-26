# Understanding IDOR (Insecure Direct Object Reference)

- IDOR Definition
IDOR, or Insecure Direct Object Reference, is a type of access control vulnerability where a web application does not verify if a user has the necessary permissions to access an object (like files or data). This occurs when a server relies too much on user-supplied input without sufficient validation.

- IDOR Example
Consider a scenario where a user accesses their profile using a URL parameter, such as http://online-service/profile?user_id=1305. If they change user_id=1305 to another ID (like user_id=1000) and access another user's data, this reveals an IDOR vulnerability due to insufficient permission checks.

## Encoded and Hashed IDs

- Encoded IDs: Many web applications use encoding, such as Base64, to transform data into ASCII-friendly formats. Users can decode and manipulate these encoded values to attempt unauthorized access.

- Hashed IDs: IDs may also be hashed using methods like MD5, creating an irreversible but consistent string for the same input. Tools like CrackStation can potentially reverse common hashes by comparing them to known values.

## Unpredictable and Hidden IDs

- Unpredictable IDs: If IDs aren’t easily guessable, it may be harder to detect IDOR. However, testers can try swapping IDs between two accounts to see if cross-access is possible, which would indicate a vulnerability.

- Locating Vulnerable Endpoints: Vulnerable endpoints may not be visible in the URL but can be found in AJAX requests or parameters within JavaScript files. Parameter mining can expose hidden fields like user_id, enabling access to other users’ data.
