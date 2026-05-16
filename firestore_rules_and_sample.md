# Firestore Rules & Sample Integration (MVP)

## What to store
Collection: `submissions`
Document id: `token` (from QR)
Fields:
- `email`: string (Google email)
- `points`: number
- `role`: string (either `M2IR` or `M2IT`)
- `recommendationResult`: string (same as role for now)
- `latestSubmission`: timestamp (Firestore Timestamp)
- `createdAt`: timestamp
- `updatedAt`: timestamp

## Firestore Security Rules (dev-friendly)
> Replace project auth rules later for production.

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    function isSignedIn() {
      return request.auth != null;
    }

    match /submissions/{token} {
      allow read: if isSignedIn() && request.auth.token.emailVerified == true;
      allow write: if isSignedIn() && request.auth.token.emailVerified == true
                   && request.resource.data.email == request.auth.token.email;
    }
  }
}
```

## QR -> MindToMajor -> Admin flow
1) QR encodes `https://<domain>/mindtomajor.html?token=<token>`
2) MindToMajor page uses Firebase Auth (Google) to login.
3) MindToMajor writes to `submissions/<token>` with email + points + derived role.
4) Admin dashboard reads `submissions` filtered by `role` to populate M2IR/M2IT.

## Admin reads (recommended)
- Query: `where('role','==','M2IR')`
- Another query for M2IT.

## Required Firebase config
- `apiKey`
- `authDomain`
- `projectId`
- `storageBucket`
- `messagingSenderId`
- `appId`

You must paste these into both pages (mindtomajor.html & index.html) or load from a safe place.

