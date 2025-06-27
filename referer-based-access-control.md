# Lab: Referer-based Access Control

##  Description
This lab demonstrates how relying on the `Referer` header for access control can be bypassed. The goal is to escalate a non-admin user to admin by exploiting flawed access control.

---

##  Objective
Promote the user `wiener` to administrator by bypassing Referer-based restrictions.

---

##  Credentials
- Admin: `administrator:admin`
- User: `wiener:peter`


##  Steps to Reproduce

1. **Login as Administrator:**
   - Use credentials: `administrator:admin`
   - Navigate to the admin panel.
   - Promote a user (e.g., `carlos`) to admin and send that HTTP request to **Burp Repeater**.

2. **Observe the Request:**
   - The promotion request looks like:
     ```
     POST /admin-roles?username=carlos&action=upgrade HTTP/1.1
     Host: <lab-id>.web-security-academy.net
     Referer: https://<lab-id>.web-security-academy.net/admin
     Cookie: session=<admin-session>
     ```

3. **Login as Non-Admin:**
   - Open a private/incognito window.
   - Log in with user: `wiener:peter`
   - Browse manually to `/admin-roles?username=carlos&action=upgrade`
   - Request fails — no `Referer` header is present.

4. **Exploit:**
   - In Burp, take the previous valid promotion request from admin, but:
     - Replace `username=carlos` with `username=wiener`
     - Replace the session cookie with the one from `wiener`’s login.
     - Ensure the `Referer` header remains the same.

5. **Send the Modified Request:**
   - Replay the request.
   - If successful, `wiener` will be promoted to an administrator.

##  Key Takeaway
Never rely on the `Referer` header for sensitive access control decisions. It's a client-controlled header and can be spoofed or replayed.

##  Mitigation
Implement robust, server-side authorization checks using sessions, roles, and permissions. Never trust headers alone for access enforcement.
