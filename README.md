# Chill Verse – Official README  
GitHub: https://github.com/YoungPresido76/Chill-verse  

A beautiful, immersive social metaverse login experience built with HTML, Tailwind CSS, and Firebase Authentication.

## Features
- Stunning glass-morphism + gradient design  
- Email/Password registration & login (real Firebase Auth)  
- Email verification required before login  
- “Forgot Password?” flow (demo alert)  
- Smooth toggle between Login ↔ Register  
- Responsive on mobile & desktop  
- Secure – no hardcoded passwords in production  

## Live Demo
https://youngpresido76.github.io/Chill-verse/  

## Tech Stack
- HTML5 + vanilla JavaScript  
- Tailwind CSS (via CDN)  
- Google Firebase Authentication (v10 compat)  
- Comfortaa Google Font  

## Project Structure
```
Chill-verse/
├── index.html         ← Main login page (this file)
├── home.html          ← Your game/dashboard (create this next)
├── README.md          ← This file
└── assets/            ← (optional) images, icons, etc.
```

## Firebase Setup (One-time)
1. Go to https://console.firebase.google.com
2. Create a new project → name it “multiverse--chill” (or any name)
3. In Project Settings → General → Your apps → Add Web App
4. Copy the firebaseConfig object
5. Replace the config in `index.html` with yours (the one currently there is already active but belongs to the original author – better to use your own)

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

6. In Firebase Console → Authentication → Sign-in method → Enable “Email/Password”

That’s it – your login will work instantly.

## Security Rules (Recommended – copy-paste these)

### Firestore Rules (if you add Firestore later)
```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Logged-in users can read anything
    allow read: if request.auth != null;
    // Users can only write their own data
    match /users/{userId} {
      allow write: if request.auth.uid == userId;
    }
    match /{document=**} {
      allow write: if false;
    }
  }
}
```

### Storage Rules (for avatars, etc.)
```js
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /avatars/{userId}/{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    match /{allPaths=**} {
      allow read, write: if false;
    }
  }
}
```

## How to Use / Test
1. Open `index.html` or the GitHub Pages link  
2. Click “Register” → create an account  
3. Check your email → click the verification link  
4. Go back → login with the same credentials  
5. You will be redirected to `home.html` (create this file for your actual game)

## Common Issues & Fixes
| Problem                          | Fix                                                                 |
|----------------------------------|----------------------------------------------------------------------|
| “Invalid account” after verify   | You still have the old mock accounts code → delete everything I showed you |
| Login button does nothing        | Make sure you used `e.preventDefault()` and `id="pass"` correctly   |
| Email verification not arriving  | Check spam folder or use a real email (not temp-mail)                |

## Future Ideas
- Add Google / Apple sign-in  
- Save username & avatar to Firestore on register  
- Add real-time chat with Firestore  
- Leaderboard, XP system, clans  

## Credits
Created with passion by **YoungPresido76**  
Design inspiration: modern metaverse login screens  
Powered by Firebase & love

## License
MIT – feel free to fork, modify, and use in your own projects (just keep the credit line if you want).

Welcome to the Chill Verse – see you inside.
