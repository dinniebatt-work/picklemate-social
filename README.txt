PICKLEMATE SOCIAL — INSTALLABLE PWA (ZERO-BUDGET STARTER)
=========================================================
This is a responsive Progressive Web App (PWA) for social pickleball. It is designed for iPhone and Android and does not use DUPR.

FILES
- index.html: app UI and matchmaking logic
- manifest.json: install metadata
- sw.js: service worker and basic offline caching
- icons/: 192px and 512px app icons

IMPORTANT: Two modes
1. Local demo mode works immediately, but data stays on the current browser/device.
2. Shared live mode needs a Firebase project configured by you. Firebase offers a no-cost Spark plan for eligible usage, but quotas and terms can change. Do not store sensitive data. This starter uses anonymous sign-in and a shared room database. Its sample rules let any authenticated anonymous user read/write rooms; anyone who gets the site URL can create an anonymous account. This is suitable only for a trusted, low-risk social-game prototype. Add stronger room authorization before public/commercial use.

PART A — CREATE FREE FIREBASE BACKEND (for shared live sessions)
1. Go to https://console.firebase.google.com and create a project (e.g. picklemate-social). Choose the no-cost Spark plan; do not add billing for this prototype.
2. In Project settings > General > Your apps, add a Web app and copy the firebaseConfig values.
3. In Build > Authentication > Sign-in method, enable Anonymous.
4. In Build > Realtime Database, create a database. Choose a nearby region. Copy its database URL.
5. In Realtime Database > Rules, use this starter rule ONLY for a trusted demo:
{
  "rules": {
    "rooms": {
      "$room": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
These rules allow every authenticated user to access all room records. Do not use for sensitive data or an untrusted public audience. For safer public use, implement per-room membership/authorization first.
6. Open index.html in a text editor. Find `const firebaseConfig = { ... }` and replace the REPLACE_WITH values with your real apiKey, authDomain, databaseURL, projectId, and appId values. Do not paste private service-account keys (the web config is not a service-account key).
7. Save index.html.

PART B — FREE HOSTING WITH GITHUB PAGES
1. Create/sign in to a GitHub account at https://github.com.
2. Create a new public repository named `picklemate-social`. Do not add a README if uploading these files directly.
3. Upload the contents of this folder to the repository root (index.html, manifest.json, sw.js, icons folder). Do not upload the ZIP file alone.
4. In repository Settings > Pages, under Build and deployment, choose Deploy from a branch. Choose `main` and `/(root)`, then Save.
5. Wait for GitHub Pages to publish. Your site URL will look like https://YOUR-USERNAME.github.io/picklemate-social/ . The actual URL depends on your username/repository. Do not assume it until GitHub shows it.
6. Open the HTTPS URL. Test adding a few demo players. Open the same URL on a second device and verify that both devices see the same session. If not, check Firebase config, Anonymous Auth, database URL, rules, and browser console.
7. Room sharing: the app uses `?room=social-main` by default. To create a separate session, change the query string, e.g. append `?room=thursday-8oct`. Share that exact URL with attendees. Keep room names non-sensitive.

PART C — INSTALL ON PHONES
iPhone (iOS): open the published HTTPS link in Safari > Share > Add to Home Screen > ensure “Open as Web App” is enabled if shown > Add.
Android: open the HTTPS link in Chrome > ⋮ menu > Install app (or Add to Home screen).
The PWA is not listed in the Apple App Store or Google Play Store. It installs directly from the website and costs nothing to distribute.
For Chrome's install prompt, the site needs HTTPS and a valid manifest with app icons. The service worker provides basic caching, but live shared data requires internet.

LIMITATIONS
- No store listing, push notifications, email/SMS, or organizer login in this starter.
- If Firebase is not configured, local demo mode is single-device only.
- Offline mode caches the shell; live session sync and score updates require internet.
- The scheduler is a heuristic: balances the skill levels (Beginner=1, Advanced beginner=2, Intermediate=3), avoids repeated teammates/opponents when possible, and rotates rests; repeats may happen depending on player count.
- Anyone with shared session access can edit names, levels, settings, scores and matches. Use first names/nicknames and only share room URLs with trusted players.
- Free hosting/backend quotas and terms may change. Review provider terms before public/commercial use.

TROUBLESHOOTING
- Blank or failed app: ensure files are in repository root and URL uses HTTPS.
- Changes do not appear: check Firebase config and Realtime Database rules; refresh the app. Service-worker cache may delay updates; increment CACHE in sw.js when publishing changes.
- Firebase `auth/operation-not-allowed`: enable Anonymous sign-in.
- Permission denied: check database rules and correct database URL.
