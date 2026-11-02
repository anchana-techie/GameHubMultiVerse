# Firebase setup (accounts, invites, admin view)

Until you finish step 3 the hub works exactly as before – nobody is asked to log in.

1. **Create the project** – https://console.firebase.google.com → *Add project* (the free Spark plan is enough).
2. **Turn on the services**
   - *Build → Authentication → Get started → Sign-in method → Email/Password → Enable* (leave "Email link" off).
   - *Authentication → Settings → Authorized domains*: add the domain you host on (and `127.0.0.1` for Live Server).
   - *Build → Firestore Database → Create database* (production mode, any region).
3. **Add your keys** – *Project settings → General → Your apps → Web app (</>)* → copy the `firebaseConfig` values into [firebase-config.js](firebase-config.js).
4. **Publish the rules** – Firestore → *Rules* → paste the contents of [firestore.rules](firestore.rules) → *Publish*. (If you change the admin e-mail, change it in both files.)
5. **Create the admin account** – open the hub → *Register* → `admin@gamehubverse.com` (no invite needed for this one address), choose a password, then click the link in the verification e-mail. The admin mailbox must be able to receive that e-mail. The first time the admin signs in, a profile with `role: admin` is created in Firestore (`users/<uid>`), so the admin is present in Firebase.
   Do this straight away – whoever registers that address first owns the admin role.
6. **Invite people** – signed in as admin: *🛡 Admin → Invite someone*. Send them the site link (the *🔗 Link* button copies an invite message). They open it, choose *Register*, use the invited e-mail, verify it, and they're in.

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
