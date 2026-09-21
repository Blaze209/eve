## 2025-05-21 - Hexadecimal IPv4-Mapped IPv6 SSRF Bypass Normalization
**Vulnerability:** IPv4-mapped IPv6 address representations in hexadecimal format (e.g. `::ffff:7f00:1` for loopback or `::ffff:a9fe:a9fe` for cloud metadata) bypassed IPv4 range checks because `normalizeAddress` only unwrapped dotted-decimal IPv4-mapped formats (`::ffff:127.0.0.1`).
**Learning:** `node:net`'s `isIP()` returns family 6 for both IPv4-mapped IPv6 forms, but `BlockList` IPv4 range checks only apply when the address is converted to standard dotted-decimal IPv4 format.
**Prevention:** Always parse and normalize hexadecimal IPv4-mapped IPv6 addresses (`::ffff:XXXX:YYYY`) into dotted-decimal IPv4 strings before evaluating network address blocklists.
