# Firebase Authentication Utility

This document contains the complete Firebase utility module and authentication functions for email & password sign-in.

---

## Configuration & Setup

Add your Firebase configuration object from the [Firebase Console](https://console.firebase.google.com/).

```javascript
const firebaseConfig = {
  apiKey: process.env.FIREBASE_API_KEY || "YOUR_API_KEY",
  authDomain: process.env.FIREBASE_AUTH_DOMAIN || "YOUR_AUTH_DOMAIN",
  projectId: process.env.FIREBASE_PROJECT_ID || "YOUR_PROJECT_ID",
  storageBucket: process.env.FIREBASE_STORAGE_BUCKET || "YOUR_STORAGE_BUCKET",
  messagingSenderId: process.env.FIREBASE_MESSAGING_SENDER_ID || "YOUR_MESSAGING_SENDER_ID",
  appId: process.env.FIREBASE_APP_ID || "YOUR_APP_ID"
};
```

---

## Utility Module Source Code

```javascript
// firebase.js implementation
import { initializeApp } from "firebase/app";
import {
  getAuth,
  signInWithEmailAndPassword,
  createUserWithEmailAndPassword,
  signOut,
  onAuthStateChanged,
  sendPasswordResetEmail
} from "firebase/auth";

// 1. Initialize Firebase App
const app = initializeApp(firebaseConfig);

// 2. Initialize Firebase Authentication
export const auth = getAuth(app);

/**
 * Sign in an existing user with email and password.
 *
 * @param {string} email - The user's email address.
 * @param {string} password - The user's password.
 * @returns {Promise<{success: boolean, user: object | null, error: {code: string, message: string} | null}>}
 */
export async function signInWithEmail(email, password) {
  try {
    const userCredential = await signInWithEmailAndPassword(auth, email, password);
    return {
      success: true,
      user: userCredential.user,
      error: null
    };
  } catch (error) {
    return {
      success: false,
      user: null,
      error: {
        code: error.code,
        message: error.message
      }
    };
  }
}

/**
 * Register a new user with email and password.
 *
 * @param {string} email - The user's email address.
 * @param {string} password - The user's chosen password.
 * @returns {Promise<{success: boolean, user: object | null, error: {code: string, message: string} | null}>}
 */
export async function signUpWithEmail(email, password) {
  try {
    const userCredential = await createUserWithEmailAndPassword(auth, email, password);
    return {
      success: true,
      user: userCredential.user,
      error: null
    };
  } catch (error) {
    return {
      success: false,
      user: null,
      error: {
        code: error.code,
        message: error.message
      }
    };
  }
}

/**
 * Sign out the currently authenticated user.
 *
 * @returns {Promise<{success: boolean, error: {code: string, message: string} | null}>}
 */
export async function logOut() {
  try {
    await signOut(auth);
    return {
      success: true,
      error: null
    };
  } catch (error) {
    return {
      success: false,
      error: {
        code: error.code,
        message: error.message
      }
    };
  }
}

/**
 * Get current user synchronously.
 *
 * @returns {object | null}
 */
export function getCurrentUser() {
  return auth.currentUser;
}

/**
 * Real-time listener for user login and logout events.
 *
 * @param {(user: object | null) => void} callback
 * @returns {() => void} Unsubscribe function
 */
export function subscribeToAuthChanges(callback) {
  return onAuthStateChanged(auth, callback);
}

/**
 * Send password reset email.
 *
 * @param {string} email
 * @returns {Promise<{success: boolean, error: {code: string, message: string} | null}>}
 */
export async function resetPassword(email) {
  try {
    await sendPasswordResetEmail(auth, email);
    return {
      success: true,
      error: null
    };
  } catch (error) {
    return {
      success: false,
      error: {
        code: error.code,
        message: error.message
      }
    };
  }
}

export default app;
```

---

## Usage Examples

### Sign In
```javascript
import { signInWithEmail } from "./firebase.js";

const { success, user, error } = await signInWithEmail("user@example.com", "SecretPass123!");

if (success) {
  console.log("Logged in UID:", user.uid);
} else {
  console.error("Login failed:", error.message);
}
```

### Sign Up
```javascript
import { signUpWithEmail } from "./firebase.js";

const { success, user, error } = await signUpWithEmail("newuser@example.com", "SecretPass123!");

if (success) {
  console.log("Registered new user:", user.email);
} else {
  console.error("Registration failed:", error.message);
}
```

### Listen to Auth State
```javascript
import { subscribeToAuthChanges } from "./firebase.js";

const unsubscribe = subscribeToAuthChanges((user) => {
  if (user) {
    console.log("Active user session:", user.email);
  } else {
    console.log("User is signed out.");
  }
});
```
