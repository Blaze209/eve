## 2025-02-23 - Timing Side-Channel in Constant-Time String Comparison

**Vulnerability:**
Webhook signature and secret-token verification functions in `linear/verify.ts`, `github/verify.ts`, and `telegram/verify.ts` checked `if (a.length !== b.length) return false;` before calling Node's `timingSafeEqual`. This short-circuited execution on length mismatch and leaked expected secret token/signature length via timing.

**Learning:**
Node's `timingSafeEqual(buf1, buf2)` throws a `RangeError` if byte lengths differ. To prevent exceptions, developers often added an early length check (`if (a.length !== b.length)`). However, checking length before comparison creates a timing side-channel where execution time varies depending on input length.

**Prevention:**
Always hash string inputs into fixed-length SHA-256 digests (`createHash("sha256").update(str).digest()`) before passing them to `timingSafeEqual`. SHA-256 converts inputs of any length into 32-byte Buffers, allowing constant-time comparison without length-check short circuits.
