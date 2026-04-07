# GLITCH - Known Limitations & Next Steps

## Known limitations at Part 3 checkpoint

- **Passcode-based QR flow**: `GuardQrScanFragment` accepts a typed pass-code instead of scanning a physical QR code with the camera; actual camera/barcode integration is not yet implemented.
- **Client-side search filtering**: `GuardSearchFragment` retrieves the latest 50 entry requests from Firestore and then filters them on the device; server-side full-text search is not supported.
- **CSV export shares raw text**: The admin audit log export (`AdminAuditLogFragment`) sends CSV content as plain text via `ACTION_SEND`; it does not write to a persisted file URI or the Downloads folder.
- **Admin profile upsert does not create Firebase Auth credentials**: `AdminUserManagementFragment` writes a Firestore `UserProfile` document but cannot create a Firebase Authentication account, so the new user cannot log in until an Auth record is manually created.
- **Guest pass expiry limited to whole hours**: `StudentGuestPassFragment` accepts only integer hour values for pass expiry; finer-grained expiry (minutes, specific timestamps) is not supported in v1.
- **No offline support**: All Firestore reads and writes require an active internet connection; Firestore offline persistence is not enabled.
- **Single concurrent session assumed**: The app does not handle or detect simultaneous logins on multiple devices for the same account.
- **No brute-force protection**: Login relies solely on Firebase Authentication password checks with no rate limiting or lockout policy implemented in the app.
- **Audit log grows unbounded**: There is no automatic purging or retention policy for access event records in Firestore.
- **Five fixed roles only**: Roles are hard-coded as `guard`, `faculty`, `staff`, `student`, and `admin`; custom or granular permission sets are not supported.

## Planned next steps

- Integrate a camera-based QR code scanner (e.g., ML Kit Barcode Scanning) to replace the passcode input in the guard QR flow.
- Move entry request search to a server-side query (Firestore composite index or a Cloud Function) to lift the 50-record client-side filtering cap.
- Save CSV exports to the device Downloads folder using `FileProvider` and a proper content URI instead of inline text sharing.
- Automate Firebase Auth account creation when the admin creates or activates a user profile, using the Firebase Admin SDK via a Cloud Function.
- Extend guest pass expiry input to accept minutes and specific date-time values.
- Enable Firestore offline persistence so guards can view recent requests during network interruptions.
- Add multi-device session handling (server-side session tokens or Firestore session documents) so concurrent logins are detected and managed.
- Implement login rate limiting and account lockout (e.g., via a Firebase App Check policy or a Cloud Function that tracks failed attempts).
- Add an automated Firestore TTL policy or scheduled Cloud Function to purge audit log entries older than a configurable retention window.
- Replace the hard-coded role set with a configurable roles/permissions collection in Firestore so new roles can be added without a code change.
