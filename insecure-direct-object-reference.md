# Lab: Insecure Direct Object References

##  Description
This lab demonstrates an insecure direct object reference (IDOR) vulnerability. The web app stores user chat logs as text files on the server, accessible via static URLs. By modifying the URL, you can access another user's chat log and extract sensitive information.

##  Objective
Find the password for the user `carlos` by exploiting the IDOR vulnerability and log into their account.

## Steps to Reproduce

1. Click on the **Live chat** tab in the application.
2. Send a dummy message and click **View transcript**.
3. Observe the URL structure used to fetch the transcript (e.g., `/files/transcript/3.txt`).
4. The filenames are numbered sequentially. Try changing the number in the URL to other values (e.g., `/files/transcript/1.txt`, `/files/transcript/2.txt`, etc.).
5. Review the contents of each file until you find the one containing the credentials for `carlos`.
6. Log in as `carlos` using the discovered password to solve the lab.

## Key Takeaways

- IDOR occurs when user-supplied input is used to access objects directly without proper authorization checks.
- Developers should enforce access control on server-side for every object access request.
- Enumerating predictable URLs can lead to unauthorized data exposure.

##  Mitigation
- Implement proper access controls.
- Use unpredictable identifiers (UUIDs) for file names or user resources.
- Validate that the user has permission to access the requested resource.
