<h1 align="center">0xRenSec</h1>

<p align="center"><b>Independent vulnerability research</b> · coordinated disclosure · every finding proven with a runnable PoC</p>

<p align="center">
  <img src="https://img.shields.io/badge/researcher-0xRenSec-0b0b0b?style=for-the-badge&logo=hackthebox&logoColor=9fef00">
  <img src="https://img.shields.io/badge/advisories-37_filed-1f6feb?style=for-the-badge&logo=github">
  <img src="https://img.shields.io/badge/runnable_PoCs-27-2ea043?style=for-the-badge">
  <img src="https://img.shields.io/badge/peak-9.8_CRITICAL-c5221f?style=for-the-badge">
  <img src="https://img.shields.io/badge/ecosystems-11-8957e5?style=for-the-badge">
  <img src="https://img.shields.io/badge/disclosure-coordinated-fb8500?style=for-the-badge">
</p>

---

```console
$ whoami
0xRenSec — independent vulnerability researcher.

I go after real bugs in software people actually run: identity / JWT verification,
SSRF guards that don't guard, deserialization sinks, wallet key generation, MCP tool
servers. Every finding here is pinned to a line of source, checked for novelty against
OSV / GHSA / NVD, and proven with a PoC I run end-to-end against the real, published
package — no theory, no "could be exploitable", no live targets. If it doesn't clear
that bar, I drop it. Credibility is the whole game.

$ cat disclosure_policy.txt
Vendor first. Loopback-only PoCs, synthetic secrets, nobody else's systems. Details
stay embargoed until there's a fix or a CVE. The Status column below tracks that live.
```

---

### ⚡ By the numbers

```text
  GitHub advisories ...... 32    Security Advisories · credit accepted
  MITRE CVEs ............. 5     requested separately
  Critical severity ...... 7     peak 9.8 — unauthenticated RCE
  Proven with a PoC ...... 27    runnable · local-only · actually executed
  Confirmed pipeline ..... 50+   novel findings across 11 ecosystems
  Malware caught ......... 8     packages across 4 supply-chain campaigns
```

---

### 🎯 Filed advisories

| # | Sev | Target | Bug | Advisory | Status |
|--:|:--:|:--|:--|:--:|:--:|
| 1 | 🔴 **9.1** | `@web5/credentials` · npm | Verifiable-Credential issuer impersonation `CWE-347` · CVSS v4.0 9.3 Critical | [GHSA-84fm-ch7f-g2r8](https://github.com/decentralized-identity/web5-js/security/advisories/GHSA-84fm-ch7f-g2r8) | 🔄 pending |
| 2 | 🔴 **9.1** | walt.id Community Stack · Maven/JVM | Credential issuer impersonation — token `x5c` cert trusted as the issuer key, no trust-anchor / `iss` binding `CWE-295` · CVSS v4.0 9.3 Critical | [GHSA-f8cq-qgpw-v6vc](https://github.com/walt-id/waltid-identity/security/advisories/GHSA-f8cq-qgpw-v6vc) | 🔄 pending |
| 3 | 🔴 **9.1** | `@solidus-network/auth` · npm | Auth bypass — VP signature verified against an attacker-controlled `proof.verificationMethod`, no binding to the holder DID → authenticate as anyone `CWE-290` · CVSS v4.0 9.3 Critical | [GHSA-hqg3-xcww-rfm7](https://github.com/solidusnetwork/sdk/security/advisories/GHSA-hqg3-xcww-rfm7) | 🔄 pending |
| 4 | 🔴 **9.1** | `auth-framework` · crates.io | Unauthenticated WebAuthn registration — no attestation / proof-of-possession → register an attacker key for any username → account takeover `CWE-306` · CVSS v4.0 9.3 Critical | [GHSA-cw9x-gg6m-9cqr](https://github.com/ciresnave/auth-framework/security/advisories/GHSA-cw9x-gg6m-9cqr) | 🔄 pending |
| 5 | 🔴 **9.8** | `flyimg/flyimg` · Composer/Docker | Unauthenticated OS command injection (RCE) — `webp-method` URL option concatenated unescaped into the ImageMagick command → `proc_open` `CWE-78` · CVSS v4.0 9.3 Critical | [GHSA-rmgv-gcwh-2pqh](https://github.com/flyimg/flyimg/security/advisories/GHSA-rmgv-gcwh-2pqh) | 🔄 pending |
| 6 | 🔴 **9.8** | Xinference (distributed) / `xoscar` · pip | Unauthenticated remote code execution — the xoscar actor-pool channel deserializes network frames with `cloudpickle.loads()` (no auth/HMAC), distributed mode binds `0.0.0.0` → one crafted pickle frame → RCE `CWE-502` · CVSS v4.0 9.3 Critical | [GHSA-jw93-m5fq-h5vc](https://github.com/xorbitsai/inference/security/advisories/GHSA-jw93-m5fq-h5vc) | 🔄 pending |
| 7 | 🟠 **8.8** | `@usex/mikrotik-mcp` · npm (MCP) | RouterOS command injection (RCE) — unconstrained tool args interpolated raw into router console commands, incl. auto-executed READ tools → arbitrary router commands via MCP prompt injection `CWE-77` · CVSS v4.0 8.7 High | [GHSA-r4cq-vhjf-mppv](https://github.com/ali-master/mikrotik-mcp/security/advisories/GHSA-r4cq-vhjf-mppv) | 🔄 pending |
| 8 | 🟠 **8.8** | `feast` · pip | Registry-server RCE (incomplete fix of CVE-2025-11157) — `ApplyMaterialization` deserializes the feature-transformation UDF with `dill.loads()` before the authorization check (the `skip_udf` hardening on `ApplyFeatureView` is missing) → authz-bypass / unauthenticated RCE `CWE-502` · CVSS v4.0 8.7 High | [GHSA-q4rh-59wh-w4jr](https://github.com/feast-dev/feast/security/advisories/GHSA-q4rh-59wh-w4jr) | 🔄 pending |
| 9 | 🟠 **8.0** | `modelscope` · pip | Model-config RCE — config YAML parsed with `yaml.load(Loader=yaml.Loader)` (mplug + TTS loaders, on the model-load path) executes `!!python/object/apply` → loading an untrusted Hub model runs code, **bypassing `trust_remote_code`**; incomplete remediation of CVE-2025-51427 `CWE-502` · CVSS v4.0 8.7 High | [GHSA-j265-4fmq-ppx6](https://github.com/modelscope/modelscope/security/advisories/GHSA-j265-4fmq-ppx6) | 🔄 pending |
| 10 | 🟠 **7.5** | `@kazuph/mcp-fetch` · npm | SSRF guard bypass → cloud-metadata `CWE-918` · CVSS v4.0 8.7 High | [GHSA-2vq8-9p6f-xwj5](https://github.com/kazuph/mcp-fetch/security/advisories/GHSA-2vq8-9p6f-xwj5) | 🔄 pending |
| 11 | 🟠 **7.5** | `web5-go` · Go | did:web issuer impersonation `CWE-347` · CVSS v4.0 8.7 High | [GHSA-vjhq-pfx7-56h5](https://github.com/decentralized-identity/web5-go/security/advisories/GHSA-vjhq-pfx7-56h5) | 🔄 pending |
| 12 | 🟠 **7.5** | `ssi` (Affinidi) · Dart/pub | JWT-VC issuer impersonation — verifying key bound to the `kid`'s own DID `CWE-347` · CVSS v4.0 8.7 High | [GHSA-ccqw-76rj-rrcq](https://github.com/affinidi/affinidi-ssi-dart/security/advisories/GHSA-ccqw-76rj-rrcq) | 🔄 pending |
| 13 | 🔴 **9.1** | `ueberauth_apple` · Hex/Elixir | "Sign in with Apple" id_token accepted with no `aud`/`iss`/`exp`/`nonce` validation → audience-confusion / replay → ATO `CWE-345` · CVSS v4.0 9.1 (v3.1 = 7.4 High) | [GHSA-pxx8-68pc-p9mr](https://github.com/ueberauth/ueberauth_apple/security/advisories/GHSA-pxx8-68pc-p9mr) | ✅ [CVE-2026-55954](https://nvd.nist.gov/vuln/detail/CVE-2026-55954) |
| 14 | 🟠 **7.4** | `Blockthon` · PyPI | Wallet private keys / mnemonics generated with non-CSPRNG Mersenne Twister on the default path → predictable keys `CWE-338` · CVSS v4.0 9.1 Critical | [GHSA-3xh6-px8p-8mvp](https://github.com/Blockthon/Blockthon/security/advisories/GHSA-3xh6-px8p-8mvp) | 🔄 pending |
| 15 | 🟠 **7.5** | `@hyperledger/identus-sdk` · npm | VP verifier never binds the presenter to the credential subject + no nonce → holder impersonation / presentation replay `CWE-294` · CVSS v4.0 8.7 High | [GHSA-9cv4-xvv9-xg8m](https://github.com/hyperledger-identus/sdk-ts/security/advisories/GHSA-9cv4-xvv9-xg8m) | 🔄 pending |
| 16 | 🟠 **7.5** | `@agledger/verify-core` · npm | Fail-open COSE verify — a 64-byte all-zero signature is accepted as "unsigned" → `valid:true` (even with the high-assurance options) `CWE-347` · CVSS v4.0 8.7 High | [GHSA-8ppx-mwp3-vvmf](https://github.com/agledger-ai/verify-core/security/advisories/GHSA-8ppx-mwp3-vvmf) | 🔄 pending |
| 17 | 🟠 **7.4** | `jwt-bearer-client-auth` · npm | JWT algorithm confusion (RS256→HS256) — asymmetric public key + mixed HS/RS allowlist on jsonwebtoken 8.x → forge client-assertions `CWE-347` · CVSS v4.0 9.1 Critical | [GHSA-vmwc-xvv7-v2xq](https://github.com/OADA/jwt-bearer-client-auth/security/advisories/GHSA-vmwc-xvv7-v2xq) | 🔄 pending |
| 18 | 🟠 **7.2** | `marqo` · pip/Docker | Unauthenticated SSRF — a search-query string is fetched as a URL gated only by a syntax-only `validators.url` check (accepts loopback / RFC-1918 / `169.254.169.254`); default `0.0.0.0:8882`, no auth → blind internal-network request forgery `CWE-918` · CVSS v4.0 6.9 Medium | [GHSA-v398-fp89-9j76](https://github.com/marqo-ai/marqo/security/advisories/GHSA-v398-fp89-9j76) | 🔄 pending |
| 19 | 🟡 **6.8** | `encrypt_shared_preferences` · pub.dev | AES-CTR with a constant IV equal to the key for every record → keystream reuse (two-time pad) + unauthenticated ciphertext `CWE-329` · CVSS v4.0 7.0 High | [GHSA-3q27-hwcf-p55w](https://github.com/xaldarof/encrypted-shared-preferences/security/advisories/GHSA-3q27-hwcf-p55w) | 🔄 pending |
| 20 | 🟡 **6.2** | `keechain` · crates.io | Bitcoin BIP39 seed encrypted at rest with an unsalted single-SHA256 password KDF → offline GPU brute-force → seed recovery `CWE-759` · CVSS v4.0 6.9 Medium | [GHSA-4f56-3j96-qp5w](https://github.com/yukibtc/keechain/security/advisories/GHSA-4f56-3j96-qp5w) | 🔄 pending |
| 21 | 🟡 **5.9** | Identus KMP SDK · Maven (Hyperledger) | VP verifier never verifies the presentation envelope signature → holder identity unauthenticated → present any victim's credential `CWE-347` · CVSS v4.0 8.2 High | [GHSA-2p4v-p249-fqjx](https://github.com/hyperledger-identus/sdk-kmp/security/advisories/GHSA-2p4v-p249-fqjx) | 🔄 pending |
| 22 | 🟠 **8.1** | `unzip-crx` / `unzip-crx-3` · npm | Zip-Slip arbitrary file write on Windows — backslash traversal in CRX entries survives jszip normalization → `path.join` escapes destination → RCE `CWE-22` · CVSS v4.0 7.2 High | [GHSA-hvqj-ph3p-f27f](https://github.com/peerigon/unzip-crx/security/advisories/GHSA-hvqj-ph3p-f27f) | 🔄 pending |
| 23 | 🟠 **8.8** | `@sworddut/mcp-ffmpeg-helper` · npm (MCP) | OS command injection (RCE) — MCP tool arguments (`extraOptions` / `options` / `format` …) are interpolated raw into a `spawn(…, {shell:true})` ffmpeg command string with no escaping or allow-list → arbitrary host command, reachable via MCP indirect prompt injection `CWE-78` · CVSS v4.0 8.7 High | MITRE — CVE pending | 🔄 pending |
| 24 | 🟠 **7.3** | `ssrfcheck` · npm | SSRF-guard bypass via NFKD parser differential — `isSSRFSafeURL()` validates the NFKD-normalized URL, but the app fetches the raw input; fullwidth `＃` / `？` fold the host boundary so the checker approves a URL whose real host is internal (loopback / RFC-1918 / `169.254.169.254`) `CWE-918` · CVSS v4.0 8.8 High | [GHSA-vjf4-72mq-xh5v](https://github.com/felippe-regazio/ssrfcheck/security/advisories/GHSA-vjf4-72mq-xh5v) | 🔄 pending |
| 25 | 🟡 **5.3** | `next-sitemap` · npm | XML injection (sitemap poisoning / content-spoofing) — core `<url>` fields (`loc`/`lastmod`/`changefreq`/`priority`) and `alternateRefs` `href`/`hreflang` are emitted unescaped while news/image/video text fields are escaped, so a dynamic sitemap built from attacker-influenced data can be poisoned with forged `<url>` entries. Served as `application/xml` → no XSS/RCE `CWE-91` · CVSS v4.0 6.9 Medium | [GHSA-xh82-92vx-jh65](https://github.com/iamvishnusankar/next-sitemap/security/advisories/GHSA-xh82-92vx-jh65) | 🔄 pending |
| 26 | 🟠 **7.3** | `dssrf` · npm | SSRF-guard bypass via NFKC parser differential — `is_url_safe()` validates the NFKC-normalized URL (and rejects userinfo / internal hosts), but the app fetches the raw input; fullwidth `＃` / `？` / `／` fold the delimiters so the checker sees host `example.com` with empty userinfo while a normal HTTP client connects to `127.0.0.1` / RFC-1918 / `169.254.169.254` — defeating the library's own userinfo guard `CWE-918` · CVSS v4.0 8.8 High | [GHSA-xx33-w569-xg7j](https://github.com/HackingRepo/dssrf-js/security/advisories/GHSA-xx33-w569-xg7j) | 🔄 pending |
| 27 | 🟠 **7.5** | `@blazity/next-image-proxy` · npm | Unauthenticated SSRF / allow-list bypass — the proxy follows 3xx redirects without re-validating the target (an allow-listed origin redirects to an internal host / `169.254.169.254` and the response is streamed back), and matches the allow-list with an unanchored regex `CWE-918` · CVSS v4.0 8.7 High | MITRE — CVE pending | 🔄 pending |
| 28 | 🟠 **7.3** | `private-ip` · npm | SSRF-guard bypass via IPv4-mapped IPv6 — `ipv6_check` matches only the dotted `::ffff:127.0.0.1`, never the hex `::ffff:7f00:1` that WHATWG `new URL()` emits, so the guard approves loopback / cloud-metadata `CWE-918` · CVSS v4.0 8.8 High | MITRE — CVE requested | 🔄 pending |
| 29 | 🟠 **8.3** | `es-toolkit` · npm | Prototype pollution in the `es-toolkit/compat` set-by-path family (`set`/`setWith`/`update`/`updateWith`) — the incomplete-safe-key guard rejects only `__proto__`, so a `constructor.prototype.<x>` path walks to `Object.prototype` and pollutes every object in the realm; re-introduces lodash CVE-2020-8203 in a package pulling ~32.3M downloads/week `CWE-1321` · CVSS v4.0 8.3 High | [GHSA-6fxx-7h6q-4x5f](https://github.com/toss/es-toolkit/security/advisories/GHSA-6fxx-7h6q-4x5f) | 🔄 pending |
| 30 | 🟠 **8.2** | `faraday-restrict-ip-addresses` · RubyGems | SSRF egress-guard bypass — the deny-list is built only from IPv4 CIDRs while the resolver returns IPv6 and `IPAddr#include?` is always false across address families, so every IPv6 destination (`::1`, ULA `fc00::/7`, `::ffff:<v4>` mapped literals incl. cloud metadata) passes `deny_rfc1918`/`deny_rfc6890` `CWE-918` · CVSS v4.0 8.8 High | MITRE — CVE requested | 🔄 pending |
| 31 | 🟠 **7.1** | `jsontokens` · npm | Signature-verification bypass — on the expanded/JWS-JSON token form `verifyExpanded` sets `verified=true` then only clears it inside a loop over the signature array, so an empty `signature:[]` vacuously passes and a fully attacker-controlled token is accepted (reachable when the consumer verifies the object form; the compact-string path is safe) `CWE-347` · CVSS v4.0 9.1 Critical (reachable path) | MITRE — CVE requested | 🔄 pending |
| 32 | 🟠 **8.8** | `prefect` · pip | Result-store pickle deserialization RCE — a persisted result / background-task-parameter record is loaded with `cloudpickle.loads` and **the stored blob names its own serializer**, so an attacker record declaring `{"type":"pickle"}` overrides a deployment configured for JSON; a lower-trust writer of a shared result / task-param store gets code execution in the reader (a task worker, or a higher-trust flow reading a poisoned cache entry) `CWE-502` · CVSS v4.0 8.6 High | [GHSA-fx6g-c8gr-xhx9](https://github.com/PrefectHQ/prefect/security/advisories/GHSA-fx6g-c8gr-xhx9) | 🔄 pending |
| 33 | 🟡 **6.5** | `dvc` · pip | Arbitrary file write outside the workspace via a malicious `.dvc` inline `outs[].files[].relpath` — `dvc pull`/`checkout`/`import` materialize an attacker-controlled directory file-list, joining each `relpath` onto the output dir with no containment check, so a `../../` entry escapes the workspace (write to an auto-run file → RCE) `CWE-22` · CVSS v4.0 6.9 Medium | [GHSA-278j-wfpv-rp8f](https://github.com/treeverse/dvc/security/advisories/GHSA-278j-wfpv-rp8f) | 🔄 pending |
| 34 | 🟡 **6.9** | `shiny` (py-shiny) · pip | py-shiny ≤ 1.6.3: unauth bookmark path traversal `CWE-22` · CVSS v4.0 6.9 Moderate | [GHSA-47c3-hpmg-7j6p](https://github.com/posit-dev/py-shiny/security/advisories/GHSA-47c3-hpmg-7j6p) | 🔄 pending |
| 35 | 🟠 **7.1** | `replicate` · pip | replicate ≤ 1.0.7: API token leak to untrusted hosts `CWE-522` · CVSS v4.0 7.1 High | [GHSA-7v25-mxqf-p9c4](https://github.com/replicate/replicate-python/security/advisories/GHSA-7v25-mxqf-p9c4) | 🔄 pending |
| 36 | 🟠 **8.5** | `@agent-infra/mcp-server-filesystem` · npm (MCP) | @agent-infra/mcp-server-filesystem ≤ 1.2.29: jail escape `CWE-22` · CVSS v4.0 8.5 High | [GHSA-c5xr-72g8-4gh8](https://github.com/bytedance/UI-TARS-desktop/security/advisories/GHSA-c5xr-72g8-4gh8) | 🔄 pending |
| 37 | 🟠 **8.7** | `modelscope` · pip | modelscope ≤ 1.38.1: video-pipeline command injection (RCE) `CWE-78` · CVSS v4.0 8.7 High | [GHSA-c69m-g9x8-gc8c](https://github.com/modelscope/modelscope/security/advisories/GHSA-c69m-g9x8-gc8c) | 🔄 pending |

<sub>Reported via GitHub Security Advisory (credit accepted), except rows 23 / 27 / 28 / 30 / 31 (MITRE-routed, no PVR). CVE IDs land on publication. The headline severity is the as-filed CVSS v3.1 Base; the `CVSS v4.0 …` note is the FIRST.org v4.0 Base recompute of the same vulnerability, cross-checked between two independent calculators. The v4.0 band can differ from the v3.1 headline — usually higher, since 4.0 drops the v3.1 Scope discount, occasionally lower for blind / subsequent-scope SSRF.</sub>

---

### 🧪 Pipeline &nbsp;<sub>`coordinated disclosure in progress — details drop on fix / CVE`</sub>

| | Count | Hunting ground |
|:--:|:--:|:--|
| 🔴 **Critical** | 6 | JWT / verifiable-credential verification bypass — alg-confusion, fail-open, issuer impersonation |
| 🟠 **High** | ~22 | RCE (`eval` / deserialization / cmd-injection), weak wallet-key KDFs, predictable-RNG keygen, SSRF, HMAC replay |
| 🟡 **Medium** | ~18 | unauthenticated / ECB / fixed-IV ciphers, weak password hashing, predictable tokens, credential gaps |
| 🦠 **Malware** | 8 pkgs | supply-chain stealers · RPC-hijacker · on-chain (EtherHiding) RCE loader |

---

### 🔬 How I work

Four filters, in order — **is it a real bug**, is it on a **reachable default path**, does the package
have **current adoption**, and is it **novel** (nothing already in OSV / GHSA / NVD). Miss any one and it
gets dropped; I'd rather ship ten findings that all hold than fifty that mostly don't. Then I write the PoC
and *run* it against the real published package — full reflection, a minted token, a command that actually
executes — not a screenshot of a code path. Every one is pinned to file:line so a maintainer can land on the
sink in seconds.

### 🤝 Disclosure

Coordinated, every time. I report privately to the maintainer first — GitHub Private Vulnerability Reporting
where it's on, MITRE where it isn't — keep the details embargoed until there's a fix or a CVE, and I never
touch a system that isn't mine. Every PoC in this portfolio runs against loopback with synthetic secrets. If
a maintainer wants the patch written too, I'll write it.

### 📡 Live tracking

The **Status** column isn't hand-edited. A tracker I wrote re-reads every GHSA in the table against GitHub's
global Advisory Database once a day and flips 🔄 → ✅ the moment a CVE is minted in my name, then pings me —
so what you're reading is current.

<sub>🔄 pending — in maintainer triage / unpublished &nbsp;·&nbsp; ✅ CVE assigned & credited to 0xRenSec &nbsp;·&nbsp; 🚫 withdrawn</sub>

---

<p align="center"><sub><code>0xRenSec</code> &nbsp;·&nbsp; coordinated disclosure &nbsp;·&nbsp; reach me through GitHub</sub></p>
