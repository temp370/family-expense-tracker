# Setup (about 10 minutes, free)
## A. Google Cloud (one time)
1. console.cloud.google.com → create a project.
2. APIs & Services → Library → enable Google Drive API.
3. OAuth consent screen: User type External, app name, your email. Scope: `.../auth/drive.file` only. Add your Gmail as a Test user (or publish to production; drive.file is a non-sensitive scope).
4. Credentials → Create credentials → OAuth client ID → Web application. Authorized JavaScript origins: `https://YOURNAME.github.io` (origin only, no path). No redirect URI and NO client secret needed.
5. Copy the Client ID and paste it in `index.html` replacing `PASTE_YOUR_CLIENT_ID.apps.googleusercontent.com`. (A Client ID is public; never put a secret in the app.)
## B. GitHub Pages
Upload all files to a repo → Settings → Pages → Deploy from branch `main` / root. Open the https URL on your phone → Chrome menu → Add to Home screen.
## C. Use
Settings → Connect Google Drive → choose your account → allow. One file `Family_Expense_Tracker.csv` is created in your Drive and updated on every sync.
## Limits
Sync runs while the app is open, on launch and when internet returns. Google tokens last ~1 hour; if it shows "Authorization required", tap Reconnect. No sync while the app is fully closed. Conflicts (same entry edited on two phones) keep the most recently edited version.
