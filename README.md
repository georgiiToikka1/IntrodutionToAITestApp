# IntrodutionToAITestApp

Firebase Authentication utility and documentation.

## Documentation Index

- [firebase.md](./firebase.md): Complete Firebase SDK utility module, helper methods (`signInWithEmail`, `signUpWithEmail`, `logOut`, `subscribeToAuthChanges`), and code examples.
- [package.md](./package.md): Project package specification, dependency configuration, and installation commands.
- [main.md](./main.md): Project overview and quick reference.

## Quick Summary of Auth Functions

| Function | Description | Parameters |
| :--- | :--- | :--- |
| `signInWithEmail` | Sign in an existing user with email and password | `(email, password)` |
| `signUpWithEmail` | Create a new user account with email and password | `(email, password)` |
| `logOut` | Sign out the active user session | None |
| `subscribeToAuthChanges` | Real-time observer for auth state changes | `(callback)` |
| `getCurrentUser` | Synchronously returns the currently authenticated user | None |
| `resetPassword` | Sends a password reset email | `(email)` |
