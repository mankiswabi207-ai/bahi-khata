# Firestore Security Rules for Hisaab

Your database is currently in "test mode," which means **anyone** can read or write to it — that's fine for the next few minutes, but must be locked down before you share the app with real users.

## What to do

1. Go to your [Firebase Console](https://console.firebase.google.com) → your project → **Build → Firestore Database → Rules** tab
2. Delete everything in the editor
3. Paste in the rules below
4. Click **Publish**

## The rules

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;

      match /{document=**} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }

    match /publicShares/{userId}/parties/{partyId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## What the new `publicShares` rule does

This supports the "Share balance link" feature — when you share a party's balance, it creates a small public document containing just that party's name and balance (no other data). Anyone with the link can view it (read: true), but only you can create or update it (write requires your own login).

## What this does

- Every signed-in user can only read and write documents under their own `users/{their-own-uid}/...` path
- No one can read or write anyone else's data, even if they know another user's ID
- Signed-out (anonymous) requests are rejected entirely

## After publishing

Test it by signing in on the app and checking that:
- Your ledgers show up
- Adding an entry saves without errors
- If you sign out and try again with a different account, you don't see the first account's data

If you ever see a "Missing or insufficient permissions" error in the browser console, it usually means these rules haven't been published yet, or the user isn't signed in when a save is attempted.
