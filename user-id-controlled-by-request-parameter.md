# Lab: User ID Controlled by Request Parameter

**Difficulty:** Apprentice  
**Category:** Access Control  

##  Summary

This lab demonstrates a **Horizontal Privilege Escalation** vulnerability where the user account page is accessed based on a user ID passed as a request parameter. The objective is to retrieve the API key of another user (`carlos`).


## Steps to Reproduce

1. Log in using the supplied credentials:  
   **Username:** `wiener`  
   **Password:** `peter`

2. Go to the account page. Observe a URL parameter like:
   /my-account/id?wiener
3. Send the request to **Burp Repeater**.

4. Modify the `id` parameter from `wiener` to `carlos`:
5. The response contains the **API key for carlos**.

6. Submit the API key to solve the lab.


##  Vulnerability Type

- Insecure Direct Object Reference (IDOR)
- Horizontal Privilege Escalation


## Mitigation

- Implement proper **access control checks** on server-side.
- Never trust user-supplied parameters like `id` for access decisions.
    
