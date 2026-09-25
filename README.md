1. Broken Access Control
Security Flaw:
The vulnerable application allows a user to request another user's profile by changing the user ID. The application does not verify whether the current user is authorized to access the requested profile.
This is an example of Broken Access Control because the application does not enforce authorization before returning protected information.
How the Fix Improves Security:
The secure version checks authorization before returning the requested profile. A normal user can access only their own profile, while an administrator can access other profiles.
OWASP Reference:
OWASP Top 10:2021 - A01: Broken Access Control

2. Broken Access Control
Security Flaw:
The vulnerable application retrieves an account using a user ID without checking whether the requester is authorized to access that account.
An attacker could potentially change the ID in the request and access another user's account information.
How the Fix Improves Security:
The secure version checks whether the requested account belongs to the current user or whether the current user has administrator privileges.
OWASP Reference:
OWASP Top 10:2021 - A01: Broken Access Control

3. Cryptographic Failures
Security Flaw:
The vulnerable code uses MD5 to hash passwords. MD5 is an outdated and inappropriate algorithm for password storage because it is designed to be very fast.
Password storage should use a password-specific hashing algorithm with a unique salt.
How the Fix Improves Security:
The secure version uses scrypt instead of MD5. It also generates a random salt for the password. This makes password cracking more difficult and prevents identical passwords from automatically having identical stored hashes.
OWASP Reference:
OWASP Top 10:2021 - A02: Cryptographic Failures

4. Cryptographic Failures
Security Flaw:
The vulnerable code uses SHA-1 to hash a password. SHA-1 is an outdated general-purpose hashing algorithm and should not be used for password storage.
Password hashing should use a password-specific algorithm designed to be computationally expensive.
How the Fix Improves Security:
The secure version uses scrypt with a unique random salt. The password is never stored directly. During login, the entered password is hashed and compared with the stored hash.
OWASP Reference:
OWASP Top 10:2021 - A02: Cryptographic Failures

5. Injection
Security Flaw:
The vulnerable code places user input directly into a SQL statement.
If the input contains SQL syntax, it can change the meaning of the database query. This is known as SQL injection.
How the Fix Improves Security:
Parameterized queries separate SQL commands from user-provided data. The database therefore treats the username as data instead of executable SQL.
OWASP Reference:
OWASP Top 10:2021 - A03: Injection

6. Injection
Security Flaw:
The original example involves a NoSQL database. The problem occurs when an application allows untrusted request data to become part of a database query.
An attacker could potentially provide a database operator instead of an ordinary username.
How the Fix Improves Security:
The secure version checks that the username is actually a string before creating the database query. This prevents an attacker from supplying a database operator where a username is expected.
OWASP Reference:
OWASP Top 10:2021 - A03: Injection

7. Insecure Design
Security Flaw:
The vulnerable password-reset process allows someone to enter an email address and immediately choose a new password.
There is no verification that the person requesting the reset actually controls the account.
This is an insecure design because the password-reset process does not contain an appropriate identity-verification step.
How the Fix Improves Security:
The secure design requires a temporary token before allowing the password to be changed. The token expires after a limited period and is deleted after it is used.
In a production application, the new password should also be securely hashed before being stored.
OWASP Reference:
OWASP Top 10:2021 - A04: Insecure Design

8. Software and Data Integrity Failures
Security Flaw:
The vulnerable example loads an external JavaScript library without verifying that the downloaded file is the expected version.
If the external file were modified, the application could potentially use malicious code.
This is a software and data integrity problem.
How the Fix Improves Security:
The application checks whether the downloaded data matches a trusted cryptographic hash. If the data has been modified, the calculated hash will not match.
For the original HTML example, the corresponding web security control is Subresource Integrity (SRI).
OWASP Reference:
OWASP Top 10:2021 - A08: Software and Data Integrity Failures

9. Server-Side Request Forgery (SSRF)
Security Flaw:
The vulnerable program allows the user to provide any URL. The server then makes a request to that URL.
An attacker could abuse this behavior to make the server request internal resources or other locations that should not be accessible.
How the Fix Improves Security:
The secure version does not allow arbitrary URLs. It requires HTTPS and checks the hostname against an allowlist.
A production application would need additional protections for DNS rebinding, redirects, IPv6, DNS resolution, and network-level access to private resources.
OWASP Reference:
OWASP Top 10:2021 - A10: Server-Side Request Forgery (SSRF)

10. Identification and Authentication Failures
Security Flaw:
The vulnerable code directly compares the password entered by the user with the stored password.
This suggests that the application stores the password in plaintext or another directly recoverable form.
Passwords should be securely hashed instead.
How the Fix Improves Security:
The secure version does not store the original password. Instead, it stores a salted password hash. When the user logs in, the entered password is hashed and compared with the stored hash.
Additional authentication protections could include rate limiting, secure session management, strong password requirements, and multifactor authentication.
OWASP Reference:
OWASP Top 10:2021 - A07: Identification and Authentication Failures
