## 2025-05-18 - Constant-Time HTTP Basic Auth Verification
**Vulnerability:** HTTP Basic auth username check used strict inequality `!==` and returned early before checking the password, introducing a timing side-channel that could leak valid usernames or string lengths.
**Learning:** `timingSafeEqual` or `timingSafeStringEquals` must be evaluated for both username and password without early return to ensure constant-time comparison across all credential fields.
**Prevention:** Always compare all authentication credential fields using timing-safe comparison functions before evaluating the overall authentication decision.
