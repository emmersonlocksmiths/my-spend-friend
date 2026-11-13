# My Spend Friend

Household spending tracker. Import Bankwest CSV exports, review and categorise every transaction, and see where the money goes. A Progressive Web App on GitHub Pages with Firebase for login and cloud sync.

## What's in it

- **Dashboard**: money in, spent and difference for a month / 3 months / 12 months; daily average and month-end projection; where the money went; spending by month; account balances; top places; biggest purchases; regular bills and subscriptions.
- **Review**: every imported transaction waits here until you confirm a category. Suggestions come from your own past choices for that place, then the built-in rules. One at a time or as a list, with undo.
- **Transactions**: search and filter everything; tap one to change its category or send it back to Review.
- **Categories**: spending per category with budgets, trends, top places and quick editing; add, rename, recolour, reorder and delete.
- **Settings**: import Bankwest CSVs (duplicates and pending transactions are skipped), accounts (nickname, type, owner, include in totals), people, suggestion rules, backup/restore.

## Firebase

Project: `my-spend-friend-9f55d` (console.firebase.google.com), Firestore in `australia-southeast1`, Email/Password sign-in, `emmersonlocksmiths.github.io` authorised.

`firestore.rules` holds the security rules. If they ever change, paste them into Firebase → Firestore → Rules and publish.

## Logins

- **First time:** on the sign-in screen tap **First-time setup** and create the main login with `nathan.emmerson@hotmail.com` (set in `index.html` as `ADMIN_EMAIL` and in `firestore.rules`). Only that email can use first-time setup.
- **Adding someone:** Settings → People → Add person (name, email, starting password). They share the household's data. **Remove** takes their access away straight away; their login can also be deleted in Firebase → Authentication → Users.
- Anyone who signs up some other way gets a "No access yet" screen, and the security rules block them from all data.
- Forgotten password: "Forgot password?" on the sign-in screen emails a reset link.

## Data layout (Firestore)

- `households/{nathanUid}`: categories, suggestion rules, accounts, recent picks, import history.
- `households/{nathanUid}/txns/{id}`: one document per transaction.
- `members/{uid}`: people Nathan has added and which household they belong to.

## Updating

The app's code and styling are all in `index.html`, so an update is normally just that file. Bump `VERSION` in `sw.js` when files change so phones pick up the new version.

## Files

| File | What it does |
|---|---|
| `index.html` | The whole app, including the Bankwest importer and the Firebase keys (these are public by design; the security rules protect the data) |
| `firestore.rules` | Security rules for Firebase → Firestore → Rules |
| `sw.js` | Lets the app open with no signal |
| `manifest.json`, `icon-*.png`, `apple-touch-icon.png`, `favicon-32.png` | App name and home-screen icon |
| `banner.jpg` | Banner at the top of the app |
