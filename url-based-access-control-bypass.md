# Lab: URL-based access control can be circumvented

## Description
This lab demonstrates how URL-based access controls can be bypassed due to misconfigured routing and reliance on front-end filtering. Although direct access to `/admin` is blocked, the backend accepts requests using the `X-Original-URL` header, allowing attackers to manipulate the intended route.

##  Objective
Access the admin panel and delete the user `carlos`.

## Steps to Reproduce

1. Try to access the `/admin` path directly — it returns a blocked or plain response.
2. Open the request in Burp Suite Repeater.
3. Modify the request line to a harmless path like `/` and add the following header: X-Original-URl: /admin

This tricks the backend into processing the request as if it's for `/admin`.
4. If successful, you'll see the admin panel.
5. To delete the user `carlos`, add the query string: username=carlos
  and update the header: X-original-URL: /admin/delete
6. Submit the request — `carlos` will be deleted, and the lab will be solved.

##  Key Takeaways

- Front-end access controls are not security mechanisms — they can be bypassed.
- Backends should implement strict authorization checks independently of request headers.
- Headers like `X-Original-URL` or `X-Rewrite-URL` can be exploited if trusted improperly.

## Tools Used
- Burp Suite (Repeater)

##  Mitigation

- Avoid trusting client-supplied headers to control routing or access logic.
- Implement proper server-side access control and authentication checks for all sensitive paths.
- Disable or sanitize headers like `X-Original-URL` if not in use.
