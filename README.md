<h1 align="center">🛡️ 0xRenSec — Security Research</h1>

<p align="center"><i>Independent vulnerability research · coordinated disclosure · zero false positives</i></p>

<p align="center">
  <img src="https://img.shields.io/badge/researcher-0xRenSec-0b0b0b?style=for-the-badge&logo=hackthebox&logoColor=9fef00">
  <img src="https://img.shields.io/badge/advisories-24_filed-1f6feb?style=for-the-badge&logo=github">
  <img src="https://img.shields.io/badge/runnable_PoCs-20-2ea043?style=for-the-badge">
  <img src="https://img.shields.io/badge/peak_severity-9.8_CRITICAL-c5221f?style=for-the-badge">
  <img src="https://img.shields.io/badge/pipeline-50%2B_findings-fb8500?style=for-the-badge">
  <img src="https://img.shields.io/badge/disclosure-coordinated-2ea043?style=for-the-badge">
</p>

---

### ⚡ By the numbers
```
  Advisories filed ........ 24  (GitHub Security Advisories, credited)  · 6 Critical · 20 with runnable PoCs
  Peak severity ........... 9.8 CRITICAL  (CVSS v3.1)
  Confirmed pipeline ...... 50+ novel findings across 11 ecosystems
  Malware caught .......... 8 packages / 4 supply-chain campaigns
  False positives shipped . 0
```

---

### 🎯 Filed advisories

| # | Sev | Target | Bug | Advisory | Status |
|--:|:--:|:--|:--|:--:|:--:|
| 1 | 🔴 **9.1** | `@web5/credentials` · npm | Verifiable-Credential issuer impersonation `CWE-347` | [GHSA-84fm-ch7f-g2r8](https://github.com/decentralized-identity/web5-js/security/advisories/GHSA-84fm-ch7f-g2r8) | 🔄 pending |
| 2 | 🔴 **9.1** | walt.id Community Stack · Maven/JVM | Credential issuer impersonation — token `x5c` cert trusted as the issuer key, no trust-anchor / `iss` binding `CWE-295` | [GHSA-f8cq-qgpw-v6vc](https://github.com/walt-id/waltid-identity/security/advisories/GHSA-f8cq-qgpw-v6vc) | 🔄 pending |
| 3 | 🔴 **9.1** | `@solidus-network/auth` · npm | Auth bypass — VP signature verified against an attacker-controlled `proof.verificationMethod`, no binding to the holder DID → authenticate as anyone `CWE-290` | [GHSA-hqg3-xcww-rfm7](https://github.com/solidusnetwork/sdk/security/advisories/GHSA-hqg3-xcww-rfm7) | 🔄 pending |
| 4 | 🔴 **9.1** | `auth-framework` · crates.io | Unauthenticated WebAuthn registration — no attestation / proof-of-possession → register an attacker key for any username → account takeover `CWE-306` | [GHSA-cw9x-gg6m-9cqr](https://github.com/ciresnave/auth-framework/security/advisories/GHSA-cw9x-gg6m-9cqr) | 🔄 pending |
| 5 | 🔴 **9.8** | `flyimg/flyimg` · Composer/Docker | Unauthenticated OS command injection (RCE) — `webp-method` URL option concatenated unescaped into the ImageMagick command → `proc_open` `CWE-78` | [GHSA-rmgv-gcwh-2pqh](https://github.com/flyimg/flyimg/security/advisories/GHSA-rmgv-gcwh-2pqh) | 🔄 pending |
| 6 | 🔴 **9.8** | Xinference (distributed) / `xoscar` · pip | Unauthenticated remote code execution — the xoscar actor-pool channel deserializes network frames with `cloudpickle.loads()` (no auth/HMAC), distributed mode binds `0.0.0.0` → one crafted pickle frame → RCE `CWE-502` | [GHSA-jw93-m5fq-h5vc](https://github.com/xorbitsai/inference/security/advisories/GHSA-jw93-m5fq-h5vc) | 🔄 pending |
| 7 | 🟠 **8.8** | `@usex/mikrotik-mcp` · npm (MCP) | RouterOS command injection (RCE) — unconstrained tool args interpolated raw into router console commands, incl. auto-executed READ tools → arbitrary router commands via MCP prompt injection `CWE-77` | [GHSA-r4cq-vhjf-mppv](https://github.com/ali-master/mikrotik-mcp/security/advisories/GHSA-r4cq-vhjf-mppv) | 🔄 pending |
| 8 | 🟠 **8.8** | `feast` · pip | Registry-server RCE (incomplete fix of CVE-2025-11157) — `ApplyMaterialization` deserializes the feature-transformation UDF with `dill.loads()` before the authorization check (the `skip_udf` hardening on `ApplyFeatureView` is missing) → authz-bypass / unauthenticated RCE `CWE-502` | [GHSA-q4rh-59wh-w4jr](https://github.com/feast-dev/feast/security/advisories/GHSA-q4rh-59wh-w4jr) | 🔄 pending |
| 9 | 🟠 **8.0** | `modelscope` · pip | Model-config RCE — config YAML parsed with `yaml.load(Loader=yaml.Loader)` (mplug + TTS loaders, on the model-load path) executes `!!python/object/apply` → loading an untrusted Hub model runs code, **bypassing `trust_remote_code`**; incomplete remediation of CVE-2025-51427 `CWE-502` | [GHSA-j265-4fmq-ppx6](https://github.com/modelscope/modelscope/security/advisories/GHSA-j265-4fmq-ppx6) | 🔄 pending |
| 10 | 🟠 **7.5** | `@kazuph/mcp-fetch` · npm | SSRF guard bypass → cloud-metadata `CWE-918` | [GHSA-2vq8-9p6f-xwj5](https://github.com/kazuph/mcp-fetch/security/advisories/GHSA-2vq8-9p6f-xwj5) | 🔄 pending |
| 11 | 🟠 **7.5** | `web5-go` · Go | did:web issuer impersonation `CWE-347` | [GHSA-vjhq-pfx7-56h5](https://github.com/decentralized-identity/web5-go/security/advisories/GHSA-vjhq-pfx7-56h5) | 🔄 pending |
| 12 | 🟠 **7.5** | `ssi` (Affinidi) · Dart/pub | JWT-VC issuer impersonation — verifying key bound to the `kid`'s own DID `CWE-347` | [GHSA-ccqw-76rj-rrcq](https://github.com/affinidi/affinidi-ssi-dart/security/advisories/GHSA-ccqw-76rj-rrcq) | 🔄 pending |
| 13 | 🟠 **7.4** | `ueberauth_apple` · Hex/Elixir | "Sign in with Apple" id_token accepted with no `aud`/`iss`/`exp`/`nonce` validation → audience-confusion / replay → ATO `CWE-345` | [GHSA-pxx8-68pc-p9mr](https://github.com/ueberauth/ueberauth_apple/security/advisories/GHSA-pxx8-68pc-p9mr) | 🔄 pending |
| 14 | 🟠 **7.4** | `Blockthon` · PyPI | Wallet private keys / mnemonics generated with non-CSPRNG Mersenne Twister on the default path → predictable keys `CWE-338` | [GHSA-3xh6-px8p-8mvp](https://github.com/Blockthon/Blockthon/security/advisories/GHSA-3xh6-px8p-8mvp) | 🔄 pending |
| 15 | 🟠 **7.5** | `@hyperledger/identus-sdk` · npm | VP verifier never binds the presenter to the credential subject + no nonce → holder impersonation / presentation replay `CWE-294` | [GHSA-9cv4-xvv9-xg8m](https://github.com/hyperledger-identus/sdk-ts/security/advisories/GHSA-9cv4-xvv9-xg8m) | 🔄 pending |
| 16 | 🟠 **7.5** | `@agledger/verify-core` · npm | Fail-open COSE verify — a 64-byte all-zero signature is accepted as "unsigned" → `valid:true` (even with the high-assurance options) `CWE-347` | [GHSA-8ppx-mwp3-vvmf](https://github.com/agledger-ai/verify-core/security/advisories/GHSA-8ppx-mwp3-vvmf) | 🔄 pending |
| 17 | 🟠 **7.4** | `jwt-bearer-client-auth` · npm | JWT algorithm confusion (RS256→HS256) — asymmetric public key + mixed HS/RS allowlist on jsonwebtoken 8.x → forge client-assertions `CWE-347` | [GHSA-vmwc-xvv7-v2xq](https://github.com/OADA/jwt-bearer-client-auth/security/advisories/GHSA-vmwc-xvv7-v2xq) | 🔄 pending |
| 18 | 🟠 **7.5** | `jose_plus` · Dart/pub.dev | JWS signature forgery — the verifier trusts an attacker-supplied embedded `jwk` header as the signing key (no binding to a trusted key) → forge any signed token; same defect as the parent `jose` (CVE-2026-34240) `CWE-347` | [GHSA-vm9r-h74p-hg97](https://github.com/Bdaya-Dev/jose/security/advisories/GHSA-vm9r-h74p-hg97) | ⚠️ review |
| 19 | 🟠 **7.2** | `marqo` · pip/Docker | Unauthenticated SSRF — a search-query string is fetched as a URL gated only by a syntax-only `validators.url` check (accepts loopback / RFC-1918 / `169.254.169.254`); default `0.0.0.0:8882`, no auth → blind internal-network request forgery `CWE-918` | [GHSA-v398-fp89-9j76](https://github.com/marqo-ai/marqo/security/advisories/GHSA-v398-fp89-9j76) | 🔄 pending |
| 20 | 🟡 **6.8** | `encrypt_shared_preferences` · pub.dev | AES-CTR with a constant IV equal to the key for every record → keystream reuse (two-time pad) + unauthenticated ciphertext `CWE-329` | [GHSA-3q27-hwcf-p55w](https://github.com/xaldarof/encrypted-shared-preferences/security/advisories/GHSA-3q27-hwcf-p55w) | 🔄 pending |
| 21 | 🟡 **6.5** | `premailer` · PyPI | Default-on SSRF — remote CSS / external resources are fetched while inlining HTML with no scheme/host restriction in the default config → reach internal services `CWE-918` | [GHSA-9pmc-p236-855h](https://github.com/peterbe/premailer/security/advisories/GHSA-9pmc-p236-855h) | 🔄 pending |
| 22 | 🟡 **6.2** | `keechain` · crates.io | Bitcoin BIP39 seed encrypted at rest with an unsalted single-SHA256 password KDF → offline GPU brute-force → seed recovery `CWE-759` | [GHSA-4f56-3j96-qp5w](https://github.com/yukibtc/keechain/security/advisories/GHSA-4f56-3j96-qp5w) | 🔄 pending |
| 23 | 🟡 **5.9** | Identus KMP SDK · Maven (Hyperledger) | VP verifier never verifies the presentation envelope signature → holder identity unauthenticated → present any victim's credential `CWE-347` | [GHSA-2p4v-p249-fqjx](https://github.com/hyperledger-identus/sdk-kmp/security/advisories/GHSA-2p4v-p249-fqjx) | 🔄 pending |
| 24 | 🟠 **8.1** | `unzip-crx` / `unzip-crx-3` · npm | Zip-Slip arbitrary file write on Windows — backslash traversal in CRX entries survives jszip normalization → `path.join` escapes destination → RCE `CWE-22` | [GHSA-hvqj-ph3p-f27f](https://github.com/peerigon/unzip-crx/security/advisories/GHSA-hvqj-ph3p-f27f) | 🔄 pending |

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

### 🔧 Methodology
**Real bug × reachable default path × current adoption × novelty** — anything that misses the bar gets dropped,
not dressed up. Every finding is pinned to file:line, checked against OSV/GHSA/NVD for novelty, proven with a
**local-only PoC** (no live exploitation, no secrets), and disclosed to the vendor first. Credibility is the flex.

<p align="center"><sub><b>0xRenSec</b> · reach out via GitHub for coordinated-disclosure matters</sub></p>
