
#  Lab: User Role Controlled by Request Parameter

**Category:** Access Control  
**Difficulty:** Apprentice  
**Lab Goal:** Delete the user `carlos` using a forged admin cookie.

##  Description

This lab demonstrates an insecure method of role-based access control where the user's privilege level (admin or normal user) is controlled via a request parameter (specifically a **cookie**). Since this value is not validated securely, an attacker can escalate privileges simply by modifying their cookie.


##  Step-by-Step Exploitation (My Explanation)

### 1. Access the Lab
- Clicked **Access the Lab**.
- Tried to visit `/admin` directly, but it said access denied.


### 2. Login as a Normal User
- Logged in using the provided credentials: (wiener:peter)
  

### 3. Intercept Login Request in Burp
- Opened **Burp Suite** and turned on **interception**.
- Went to the login page and submitted the credentials.
- Captured the **login response** in Burp (intercept response ON).


### 4. Modify the Cookie in Response
- Set-Cookie: admin=false to Set-cookie: admin=true
- Forword the request
- - This time, access was **granted** because the admin cookie was now `true`.


### 6. Delete User carlos
- On the admin panel, clicked **Delete** next to user `carlos`.

✅ Lab completed — user `carlos` was deleted successfully.

---

## 📌 Why This Works

- The application trusts a **client-controlled cookie** (`Admin=true`) to determine if a user is an admin.
- This cookie value is **not validated** on the server.
- Any logged-in user can escalate privileges by modifying the cookie.


##  Mitigation

- Never rely on user-controlled parameters (like cookies or URLs) to decide access level.
- Store user roles server-side and validate them based on **authenticated session IDs**.
- Implement proper access control checks in backend logic.


##  Key Takeaways

- Access control should be **enforced on the server**, not the client.
- Cookies are easily modifiable by users and cannot be trusted.
- Always test for insecure direct object references and role tampering using tools like Burp Suite.


>  This lab shows how a simple logic flaw in trust can lead to full privilege escalation.
