<h1 align="center">🛡️ 0xRenSec — Security Research</h1>

<p align="center"><i>Independent vulnerability research · coordinated disclosure · zero false positives</i></p>

<p align="center">
  <img src="https://img.shields.io/badge/researcher-0xRenSec-0b0b0b?style=for-the-badge&logo=hackthebox&logoColor=9fef00">
  <img src="https://img.shields.io/badge/advisories-18_filed-1f6feb?style=for-the-badge&logo=github">
  <img src="https://img.shields.io/badge/runnable_PoCs-14-2ea043?style=for-the-badge">
  <img src="https://img.shields.io/badge/peak_severity-9.1_CRITICAL-c5221f?style=for-the-badge">
  <img src="https://img.shields.io/badge/pipeline-50%2B_findings-fb8500?style=for-the-badge">
  <img src="https://img.shields.io/badge/disclosure-coordinated-2ea043?style=for-the-badge">
</p>

---

### ⚡ By the numbers
```
  Advisories filed ........ 18  (GitHub Security Advisories, credited)  · 5 Critical · 14 with runnable PoCs
  Peak severity ........... 9.1 CRITICAL  (CVSS v3.1)
  Confirmed pipeline ...... 50+ novel findings across 11 ecosystems
  Malware caught .......... 8 packages / 4 supply-chain campaigns
  False positives shipped . 0
```

---

### 🎯 Filed advisories

| Sev | Target | Bug | Advisory |
|:--:|:--|:--|:--:|
| 🔴 **9.1** | `@web5/credentials` · npm | Verifiable-Credential issuer impersonation `CWE-347` | [GHSA-84fm-ch7f-g2r8](https://github.com/decentralized-identity/web5-js/security/advisories/GHSA-84fm-ch7f-g2r8) |
| 🔴 **9.1** | walt.id Community Stack · Maven/JVM | Credential issuer impersonation — token `x5c` cert trusted as the issuer key, no trust-anchor / `iss` binding `CWE-295` | [GHSA-f8cq-qgpw-v6vc](https://github.com/walt-id/waltid-identity/security/advisories/GHSA-f8cq-qgpw-v6vc) |
| 🔴 **9.1** | `@solidus-network/auth` · npm | Auth bypass — VP signature verified against an attacker-controlled `proof.verificationMethod`, no binding to the holder DID → authenticate as anyone `CWE-290` | [GHSA-hqg3-xcww-rfm7](https://github.com/solidusnetwork/sdk/security/advisories/GHSA-hqg3-xcww-rfm7) |
| 🔴 **9.1** | `auth-framework` · crates.io | Unauthenticated WebAuthn registration — no attestation / proof-of-possession → register an attacker key for any username → account takeover `CWE-306` | [GHSA-cw9x-gg6m-9cqr](https://github.com/ciresnave/auth-framework/security/advisories/GHSA-cw9x-gg6m-9cqr) |
| 🔴 **9.8** | `flyimg/flyimg` · Composer/Docker | Unauthenticated OS command injection (RCE) — `webp-method` URL option concatenated unescaped into the ImageMagick command → `proc_open` `CWE-78` | [GHSA-rmgv-gcwh-2pqh](https://github.com/flyimg/flyimg/security/advisories/GHSA-rmgv-gcwh-2pqh) |
| 🟠 **8.8** | `@usex/mikrotik-mcp` · npm (MCP) | RouterOS command injection (RCE) — unconstrained tool args interpolated raw into router console commands, incl. auto-executed READ tools → arbitrary router commands via MCP prompt injection `CWE-77` | [GHSA-r4cq-vhjf-mppv](https://github.com/ali-master/mikrotik-mcp/security/advisories/GHSA-r4cq-vhjf-mppv) |
| 🟠 **7.5** | `@kazuph/mcp-fetch` · npm | SSRF guard bypass → cloud-metadata `CWE-918` | [GHSA-2vq8-9p6f-xwj5](https://github.com/kazuph/mcp-fetch/security/advisories/GHSA-2vq8-9p6f-xwj5) |
| 🟠 **7.5** | `web5-go` · Go | did:web issuer impersonation `CWE-347` | [GHSA-vjhq-pfx7-56h5](https://github.com/decentralized-identity/web5-go/security/advisories/GHSA-vjhq-pfx7-56h5) |
| 🟠 **7.5** | `ssi` (Affinidi) · Dart/pub | JWT-VC issuer impersonation — verifying key bound to the `kid`'s own DID `CWE-347` | [GHSA-ccqw-76rj-rrcq](https://github.com/affinidi/affinidi-ssi-dart/security/advisories/GHSA-ccqw-76rj-rrcq) |
| 🟠 **7.4** | `ueberauth_apple` · Hex/Elixir | "Sign in with Apple" id_token accepted with no `aud`/`iss`/`exp`/`nonce` validation → audience-confusion / replay → ATO `CWE-345` | [GHSA-pxx8-68pc-p9mr](https://github.com/ueberauth/ueberauth_apple/security/advisories/GHSA-pxx8-68pc-p9mr) |
| 🟠 **7.4** | `Blockthon` · PyPI | Wallet private keys / mnemonics generated with non-CSPRNG Mersenne Twister on the default path → predictable keys `CWE-338` | [GHSA-3xh6-px8p-8mvp](https://github.com/Blockthon/Blockthon/security/advisories/GHSA-3xh6-px8p-8mvp) |
| 🟠 **7.5** | `@hyperledger/identus-sdk` · npm | VP verifier never binds the presenter to the credential subject + no nonce → holder impersonation / presentation replay `CWE-294` | [GHSA-9cv4-xvv9-xg8m](https://github.com/hyperledger-identus/sdk-ts/security/advisories/GHSA-9cv4-xvv9-xg8m) |
| 🟠 **7.5** | `@agledger/verify-core` · npm | Fail-open COSE verify — a 64-byte all-zero signature is accepted as "unsigned" → `valid:true` (even with the high-assurance options) `CWE-347` | [GHSA-8ppx-mwp3-vvmf](https://github.com/agledger-ai/verify-core/security/advisories/GHSA-8ppx-mwp3-vvmf) |
| 🟠 **7.4** | `jwt-bearer-client-auth` · npm | JWT algorithm confusion (RS256→HS256) — asymmetric public key + mixed HS/RS allowlist on jsonwebtoken 8.x → forge client-assertions `CWE-347` | [GHSA-vmwc-xvv7-v2xq](https://github.com/OADA/jwt-bearer-client-auth/security/advisories/GHSA-vmwc-xvv7-v2xq) |
| 🟡 **6.8** | `encrypt_shared_preferences` · pub.dev | AES-CTR with a constant IV equal to the key for every record → keystream reuse (two-time pad) + unauthenticated ciphertext `CWE-329` | [GHSA-3q27-hwcf-p55w](https://github.com/xaldarof/encrypted-shared-preferences/security/advisories/GHSA-3q27-hwcf-p55w) |
| 🟡 **6.2** | `keechain` · crates.io | Bitcoin BIP39 seed encrypted at rest with an unsalted single-SHA256 password KDF → offline GPU brute-force → seed recovery `CWE-759` | [GHSA-4f56-3j96-qp5w](https://github.com/yukibtc/keechain/security/advisories/GHSA-4f56-3j96-qp5w) |
| 🟡 **5.9** | Identus KMP SDK · Maven (Hyperledger) | VP verifier never verifies the presentation envelope signature → holder identity unauthenticated → present any victim's credential `CWE-347` | [GHSA-2p4v-p249-fqjx](https://github.com/hyperledger-identus/sdk-kmp/security/advisories/GHSA-2p4v-p249-fqjx) |
| 🟠 **8.1** | `unzip-crx` / `unzip-crx-3` · npm | Zip-Slip arbitrary file write on Windows — backslash traversal in CRX entries survives jszip normalization → `path.join` escapes destination → RCE `CWE-22` | [GHSA-hvqj-ph3p-f27f](https://github.com/peerigon/unzip-crx/security/advisories/GHSA-hvqj-ph3p-f27f) |

<sub>Reported via GitHub Security Advisory, credit accepted. CVE IDs land on maintainer publication.</sub>

---

### 🧪 Pipeline `(coordinated disclosure in progress — details drop on fix/CVE)`

| | Count | Hunting ground |
|:--:|:--:|:--|
| 🔴 **Critical** | 6 | JWT / verifiable-credential verification bypass — alg-confusion, fail-open, issuer impersonation |
| 🟠 **High** | ~22 | RCE (`eval` / deserialization / cmd-injection), weak wallet-key KDFs, predictable-RNG keygen, SSRF, HMAC replay |
| 🟡 **Medium** | ~18 | unauthenticated / ECB / fixed-IV ciphers, weak password hashing, predictable tokens, credential gaps |
| 🦠 **Malware** | 8 pkgs | supply-chain stealers · RPC-hijacker · on-chain (EtherHiding) RCE loader |

---

### 🔧 How I work
**Real bug × reachable default path × current adoption × novelty** — anything that misses the bar gets dropped,
not dressed up. Every finding is pinned to file:line, checked against OSV/GHSA/NVD for novelty, proven with a
**local-only PoC** (no live exploitation, no secrets), and disclosed to the vendor first. Credibility is the flex.

<p align="center"><sub><b>0xRenSec</b> · reach out via GitHub for coordinated-disclosure matters</sub></p>
