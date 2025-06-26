# Lab: User Role Can Be Modified in User Profile

##  Description
This lab demonstrates an Insecure Direct Object Reference (IDOR) vulnerability in user roles. The application allows users to update their account information via a JSON API. However, it fails to enforce server-side authorization on sensitive attributes such as `roleid`, allowing privilege escalation.

**Goal:** Access the `/admin` panel and delete the user `carlos`.


##  Steps to Reproduce

1. **Login** using the provided credentials: (wiener:peter)
2. **Navigate** to the account settings page where you can change your email.

3. **Intercept** the email update request using **Burp Suite**.

4. **Modify the JSON body** of the request in **Burp Repeater** to include:
```json
{
  "email": "attacker@exploit.com",
  "roleid": 2
}
5. Forward the request and verify that the response shows roleid is now 2.
6. Access the admin panel at: /admin
7. delete the user carlos to solve the lab.


##  Key Takeaways

- Always validate roles on the **server-side**.
- Never trust client-side data like `roleid`.
- Classic example of **IDOR** vulnerability.
- Enforce proper **access controls** on sensitive actions.
