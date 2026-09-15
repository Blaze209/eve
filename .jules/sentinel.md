## 2025-09-15 - Constant-time comparison for HTTP Basic credentials
**Vulnerability:** HTTP Basic strategy compared usernames using standard non-constant-time equality (`!==`) with an early return before hashing and comparing passwords.
**Learning:** Short-circuiting username equality before password evaluation creates a timing side-channel that leaks username validity to unauthenticated attackers.
**Prevention:** Always compare both username and password using constant-time equality (`timingSafeStringEquals`) and evaluate both unconditionally before rejecting invalid credentials.
