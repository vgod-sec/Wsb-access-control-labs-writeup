## Lab: Unprotected Admin Functionality

**Goal:** Delete user `carlos` via unprotected admin panel.

### 🛠️ Steps:
1. Visit `/robots.txt` to find hidden admin path.
2. Go to `/administrator-panel` (found in Disallow).
3. Delete `carlos` user.

### Key Point:
Never expose admin functions without proper access control.
`robots.txt` shouldn't be used to hide sensitive paths.
