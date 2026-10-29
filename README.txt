# PickleMate Social — New Interface

## Included
- Reclub-inspired responsive interface for Home, Games, History, Community, Profile and Venues.
- Create game, join game, add players/venues, edit profile and record scores.
- Match history shows date, venue, time, result, score and player names.
- Win/loss statistics and CSV export.
- PWA manifest, service worker and app icons.

## Update your existing GitHub Pages website
1. Open your `picklemate-social` repository on GitHub.
2. Click **Add file → Upload files**.
3. Upload/replace `index.html`, `manifest.json`, `sw.js`, and the `icons` folder from this ZIP.
4. Click **Commit changes** at the bottom.
5. Wait 1–3 minutes and refresh your published website. If the old version remains, try Ctrl+F5 or close and reopen the installed app.

## Important
This is a front-end prototype and saves data only in the current browser using local storage. Demo match history is included to show the layout; replace it with real records before public use. It does NOT sync across phones yet. Firebase connection and secure per-room access rules must be implemented before shared use. Avoid entering sensitive personal information.
