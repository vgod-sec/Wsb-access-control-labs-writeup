# Lab: Multi-step process with no access control on one step

##  Description
This lab demonstrates a vulnerability in multi-step access control logic. While some steps in the privilege escalation process are protected, at least one step lacks proper access control. This allows a low-privileged user to bypass restrictions and become an administrator.

## Objective
Exploit the flawed access control in the multi-step admin role assignment process to escalate your user privileges.

##  Steps to Reproduce

1. Log in as the admin using: administrator:admin
2. Promote the user `carlos` to admin and capture the promotion request using Burp Suite.
3. Open a private/incognito window and log in as: wiener:peter
4. Take the Burp Repeater request from step 2 and replace the session cookie with `wiener:peter`'s session.
5. Try sending the same promotion request — you’ll receive `Unauthorized`.
6. Modify the method from `POST` to something invalid like `POSTX` — you’ll get a `Missing parameter` error, meaning the backend is responding.
7. Change the method to `GET` using Burp's "Change request method" option.
8. Replace the `username` value with your own (`wiener`) and resend the request.
9. If successful, you’ll be promoted to admin and solve the lab.

##  Key Takeaways

- Multi-step processes must have access control enforced on **every** step, not just the entry point.
- Attackers can reuse or modify captured requests with different methods or headers to bypass access control.
- Always validate user permissions **server-side** at **each** functional endpoint.

##  Mitigation

- Apply consistent role and permission checks across **every request handler**.
- Avoid relying on front-end validation or client behavior to enforce security rules.
- Use secure design patterns for multi-step operations, such as server-side state tracking and role verification.
