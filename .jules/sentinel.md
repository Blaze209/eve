## 2025-02-28 - Constant-Time String Comparison in Webhook Verification
**Vulnerability:** Timing side-channel leak in `constantTimeCompare` when verifying webhook signatures and secret tokens across linear, github, and telegram channels. Early return on string length mismatch (`if (a.length !== b.length) return false`) and variable-length string comparisons exposed timing information.
**Learning:** `timingSafeEqual` in Node.js throws if Buffer lengths differ, leading to dangerous length pre-checks in custom `constantTimeCompare` functions.
**Prevention:** Always hash strings to fixed-length SHA-256 digests (`createHash("sha256").update(str).digest()`) prior to `timingSafeEqual` comparison to guarantee constant-time evaluation without length leaks or exception paths.
