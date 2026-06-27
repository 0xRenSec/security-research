# Security Research — 0xRenSec

Independent vulnerability research, conducted under **coordinated / responsible disclosure**.
All findings are identified by static source review + local-only proofs of concept — no live systems
are exploited and no secrets are used. Full technical detail for each finding is published **only after
the vendor ships a fix or a CVE is assigned**; everything still under embargo is summarised here without
exploitable specifics.

**Researcher:** 0xRenSec · **Disclosure venues:** GitHub Security Advisories (where the repo accepts reports), else MITRE CVE requests; malware reported to the relevant registry.

---
## Filed advisories
Security advisories reported and credited to **0xRenSec** (currently in maintainer triage — links open to
collaborators until the maintainers publish):

| Advisory | Ecosystem | Severity | Class | Status |
|---|---|---|---|---|
| [GHSA-2vq8-9p6f-xwj5](https://github.com/kazuph/mcp-fetch/security/advisories/GHSA-2vq8-9p6f-xwj5) — `@kazuph/mcp-fetch` | npm | 🟠 High (7.5) | SSRF guard bypass (IPv4-mapped IPv6) → cloud-metadata access (CWE-918) | Reported · credit accepted · awaiting publication |
| [GHSA-84fm-ch7f-g2r8](https://github.com/decentralized-identity/web5-js/security/advisories/GHSA-84fm-ch7f-g2r8) — `@web5/credentials` | npm | 🔴 Critical (9.1) | Verifiable-Credential issuer impersonation (CWE-347/290) | Reported · credit accepted · awaiting publication |

CVE IDs will appear here once the advisories are published.

---
## Research pipeline (under coordinated disclosure — details withheld)
Confirmed, novel findings currently being disclosed responsibly. **Package names and exploit detail are
intentionally withheld** until each vendor is notified and a fix/CVE lands; entries graduate to the
**Filed advisories** table above (with full names + links) as they are disclosed.

| Severity | Count | Representative classes (no packages named) |
|---|---|---|
| 🔴 Critical | 6 | JWT / verifiable-credential verification bypass — algorithm confusion, fail-open signature checks, issuer impersonation |
| 🟠 High | ~22 | RCE (unsafe `eval` / deserialization / command-injection), weak wallet-key KDFs, predictable-RNG key generation, SSRF, HMAC replay |
| 🟡 Medium | ~18 | unauthenticated / ECB / fixed-IV cipher modes, weak password hashing, predictable security tokens, credential-verification gaps |
| 🦠 Malware | 8 pkgs / 4 campaigns | supply-chain stealers, RPC-hijacker, on-chain (EtherHiding) RCE loader — reported to the registry |

Each is file:line-evidenced, novelty-checked against public advisory databases, and CVSS-scored with honest caveats.

---
## Approach
- **Impact bar:** every finding is filtered on *real bug × reachable default path × current adoption × novelty*. Weak, already-known, or by-design behaviours are dropped honestly rather than inflated.
- **Verification:** static review at the exact file/line, plus local-only PoCs (no live exploitation, no real credentials).
- **Disclosure ethics:** vendors first; public detail only after a fix or CVE. This page is updated as disclosures progress.

_Maintained by 0xRenSec. Reach out via GitHub for coordinated-disclosure matters._
