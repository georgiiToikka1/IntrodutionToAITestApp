# Project Overview & Firebase Authentication Guide

This repository contains the Firebase authentication utility and configuration converted into markdown documentation.

## Documentation Index

- [firebase.md](file:///c:/antigravity%20app/test/firebase.md): Complete Firebase SDK utility module, helper methods (`signInWithEmail`, `signUpWithEmail`, `logOut`, `subscribeToAuthChanges`), and code examples.
- [package.md](file:///c:/antigravity%20app/test/package.md): Project package specification, dependency configuration, and installation commands.

---

## Quick Summary of Auth Functions

| Function | Description | Parameters |
| :--- | :--- | :--- |
| `signInWithEmail` | Sign in an existing user with email and password | `(email, password)` |
| `signUpWithEmail` | Create a new user account with email and password | `(email, password)` |
| `logOut` | Sign out the active user session | None |
| `subscribeToAuthChanges` | Real-time observer for auth state changes | `(callback)` |
| `getCurrentUser` | Synchronously returns the currently authenticated user | None |
| `resetPassword` | Sends a password reset email | `(email)` |

For full code implementations and copy-pasteable snippets, see [firebase.md](file:///c:/antigravity%20app/test/firebase.md).
