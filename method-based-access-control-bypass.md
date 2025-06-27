# Lab: Method-based access control can be circumvented

##  Description
This lab demonstrates how access control mechanisms relying solely on HTTP methods (e.g., GET vs POST) can be bypassed. While the front-end restricts certain actions based on the HTTP method, the backend fails to enforce method-based access control securely.

##  Objective
Log in using the provided user credentials and escalate privileges by bypassing method-based restrictions to become an administrator.

##  Steps to Reproduce

1. Log in with the credentials: wiener:peter
2. Navigate to the user account page.
3. Inspect the functionality that performs admin privilege changes and note that it's blocked via the UI for non-admins.
4. Use Burp Suite to intercept the request and note the method (likely POST or GET).
5. Change the method to the one not allowed via the UI (e.g., switch from GET to POST).
6. Modify the request body or query to include: role=administrator
7. Forward the request — the backend fails to validate the method and promotes the user to admin.
8. Confirm admin privileges and complete the lab.

##  Key Takeaways

- Relying solely on HTTP methods (like GET or POST) for access control is insecure.
- Authorization should be enforced based on user roles on the server side — not based on request methods.
- Attackers can easily change the HTTP method using tools like Burp Suite.

##  Tools Used

- Burp Suite (Proxy, Repeater)

##  Mitigation

- Implement proper server-side role-based access control (RBAC).
- Never trust client-side or method-based restrictions alone.
- Validate user permissions on every request, regardless of method. 
