# Sentinel Journal

## 2025-09-27 - Constant-time comparison for HTTP Basic Auth username verification
**Vulnerability:** Timing side-channel leakage in HTTP Basic Auth username check (`normalizeCredential(username) !== normalizeCredential(strategyUsername)` returned early on mismatch before running constant-time password check).
**Learning:** Checking username using non-constant-time comparison prior to password verification allows attackers to perform timing attacks (username enumeration).
**Prevention:** Compare both username and password credentials using `timingSafeEqual` in constant time before deciding authentication status.
