# Firebase setup (accounts, invites, admin view)

Until you finish step 3 the hub works exactly as before – nobody is asked to log in.

1. **Create the project** – https://console.firebase.google.com → *Add project* (the free Spark plan is enough).
2. **Turn on the services**
   - *Build → Authentication → Get started → Sign-in method → Email/Password → Enable* (leave "Email link" off).
   - *Authentication → Settings → Authorized domains*: add the domain you host on (and `127.0.0.1` for Live Server).
   - *Build → Firestore Database → Create database* (production mode, any region).
3. **Add your keys** – *Project settings → General → Your apps → Web app (</>)* → copy the `firebaseConfig` values into [firebase-config.js](firebase-config.js).
4. **Publish the rules** – Firestore → *Rules* → paste the contents of [firestore.rules](firestore.rules) → *Publish*. 
5. **Create the admin** – admin is a *role* on the profile (`users/<uid>` with `role: "admin"`), the same idea as the `members` collection in your other project.
   1. Firebase → *Authentication → Users → Add user*: e-mail `admin@gamehubverse.com` + a password. Copy the new user's **User UID**.
   2. *Firestore → Start collection* `users` → document ID = that UID, with fields: `email` (string) `admin@gamehubverse.com`, `name` (string) `Admin`, `role` (string) `admin`.
   3. Open the hub and sign in – the 🛡 Admin button appears. Add a recovery question under *📊 My activity → 🔐 Password recovery*.
   Later, the admin can make any registered person an admin (or remove the role) from the Admin view (*⭐ Make admin*).
6. **Invite people** – signed in as admin: *🛡 Admin → Invite someone*. Send them the site link (the *🔗 Link* button copies an invite message). They open it, choose *Register*, use the invited e-mail, pick a password and a recovery question, and they're in.

## How it works
| Thing | Where |
|---|---|
| Who may register | `invites/<email>` (status `invited` / `registered` / `removed`) – checked by the app **and** by the Firestore rules |
| Profile, last sign-in, sign-in count, online/last seen, device | `users/<uid>` |
| Per-game played / hosted / finished / wins / points / time | `users/<uid>.stats.<game>` |
| Recent activity (sign-ins and games) | `users/<uid>/activity/*` |

**Removing an account** (admin view → *🗑 Remove*): the profile and activity are deleted and the invite becomes `removed`. The person loses all access immediately (their open page signs them out), cannot register again until re-invited, and their leftover sign-in record is deleted automatically the next time they try to sign in. (Deleting someone else's sign-in record directly needs Cloud Functions / the Admin SDK, so the app doesn't do it.)

**Notes**
- Anyone can look up whether a specific e-mail is invited (needed to validate registration) but cannot list invites.
- Game stats are written by each player's own browser, so they are trustworthy for a friends group but not tamper-proof.
- Online status uses a 60-second heartbeat while the page is open.

## Forgotten passwords (no e-mail needed)
At registration each person picks a recovery question and answer. *Forgot password* asks for their e-mail and the answer, then lets them choose a new password. The answer is never stored: the password is kept encrypted under a key derived from it (`recovery/<email>`), so a **strong, hard-to-guess answer matters** – anyone who can guess it can take the account. Existing accounts (like the admin) can add a question under *📊 My activity → 🔐 Password recovery*. Removing an account also deletes its recovery record.
