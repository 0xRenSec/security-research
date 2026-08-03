<h1 align="center">0xRenSec</h1>

<p align="center"><b>Independent vulnerability research</b> · coordinated disclosure · every finding proven with a runnable PoC</p>

<p align="center">
  <img src="https://img.shields.io/badge/researcher-0xRenSec-0b0b0b?style=for-the-badge&logo=hackthebox&logoColor=9fef00">
  <img src="https://img.shields.io/badge/advisories-57_filed-1f6feb?style=for-the-badge&logo=github">
  <img src="https://img.shields.io/badge/runnable_PoCs-55-2ea043?style=for-the-badge">
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
  GitHub advisories ...... 52    Security Advisories · credit accepted
  MITRE CVEs ............. 5     requested separately
  Critical severity ...... 7     peak 9.8 — unauthenticated RCE
  Proven with a PoC ...... 55    runnable · local-only · of 57 filed (2 unverified)
  Confirmed pipeline ..... 50+   novel findings across 11 ecosystems
  Malware caught ......... 8     packages across 4 supply-chain campaigns
```

---

### 🎯 Filed advisories

| # | Sev | Target | Bug | Advisory | Status |
|--:|:--:|:--|:--|:--:|:--:|
| 1 | 🔴 **9.3** | `@web5/credentials` · npm | Verifiable-Credential issuer impersonation `CWE-347` | [GHSA-84fm-ch7f-g2r8](https://github.com/decentralized-identity/web5-js/security/advisories/GHSA-84fm-ch7f-g2r8) | 🔄 pending |
| 2 | 🔴 **9.3** | walt.id Community Stack · Maven/JVM | Credential issuer impersonation — token `x5c` cert trusted as the issuer key, no trust-anchor / `iss` binding `CWE-295` | [GHSA-f8cq-qgpw-v6vc](https://github.com/walt-id/waltid-identity/security/advisories/GHSA-f8cq-qgpw-v6vc) | 🔄 pending |
| 3 | 🔴 **9.3** | `@solidus-network/auth` · npm | Auth bypass — VP signature verified against an attacker-controlled `proof.verificationMethod`, no binding to the holder DID → authenticate as anyone `CWE-290` | [GHSA-hqg3-xcww-rfm7](https://github.com/solidusnetwork/sdk/security/advisories/GHSA-hqg3-xcww-rfm7) | 🔄 pending |
| 4 | 🔴 **9.3** | `auth-framework` · crates.io | Unauthenticated WebAuthn registration — no attestation / proof-of-possession → register an attacker key for any username → account takeover `CWE-306` | [GHSA-cw9x-gg6m-9cqr](https://github.com/ciresnave/auth-framework/security/advisories/GHSA-cw9x-gg6m-9cqr) | 🔄 pending |
| 5 | 🔴 **9.3** | `flyimg/flyimg` · Composer/Docker | Unauthenticated OS command injection (RCE) — `webp-method` URL option concatenated unescaped into the ImageMagick command → `proc_open` `CWE-78` | [GHSA-rmgv-gcwh-2pqh](https://github.com/flyimg/flyimg/security/advisories/GHSA-rmgv-gcwh-2pqh) | ✅ [CVE-2026-63656](https://nvd.nist.gov/vuln/detail/CVE-2026-63656) |
| 6 | 🔴 **9.3** | Xinference (distributed) / `xoscar` · pip | Unauthenticated remote code execution — the xoscar actor-pool channel deserializes network frames with `cloudpickle.loads()` (no auth/HMAC), distributed mode binds `0.0.0.0` → one crafted pickle frame → RCE `CWE-502` | [GHSA-jw93-m5fq-h5vc](https://github.com/xorbitsai/inference/security/advisories/GHSA-jw93-m5fq-h5vc) | 🔄 pending |
| 7 | 🟠 **8.7** | `@usex/mikrotik-mcp` · npm (MCP) | RouterOS command injection (RCE) — unconstrained tool args interpolated raw into router console commands, incl. auto-executed READ tools → arbitrary router commands via MCP prompt injection `CWE-77` | [GHSA-r4cq-vhjf-mppv](https://github.com/ali-master/mikrotik-mcp/security/advisories/GHSA-r4cq-vhjf-mppv) | 🔄 pending |
| 8 | 🟠 **8.7** | `feast` · pip | Registry-server RCE (incomplete fix of CVE-2025-11157) — `ApplyMaterialization` deserializes the feature-transformation UDF with `dill.loads()` before the authorization check (the `skip_udf` hardening on `ApplyFeatureView` is missing) → authz-bypass / unauthenticated RCE `CWE-502` | [GHSA-q4rh-59wh-w4jr](https://github.com/feast-dev/feast/security/advisories/GHSA-q4rh-59wh-w4jr) | 🔄 pending |
| 9 | 🟠 **8.7** | `modelscope` · pip | Model-config RCE — config YAML parsed with `yaml.load(Loader=yaml.Loader)` (mplug + TTS loaders, on the model-load path) executes `!!python/object/apply` → loading an untrusted Hub model runs code, **bypassing `trust_remote_code`**; incomplete remediation of CVE-2025-51427 `CWE-502` | [GHSA-j265-4fmq-ppx6](https://github.com/modelscope/modelscope/security/advisories/GHSA-j265-4fmq-ppx6) | 🔄 pending |
| 10 | 🟠 **8.7** | `@kazuph/mcp-fetch` · npm | SSRF guard bypass → cloud-metadata `CWE-918` | [GHSA-2vq8-9p6f-xwj5](https://github.com/kazuph/mcp-fetch/security/advisories/GHSA-2vq8-9p6f-xwj5) | 🔄 pending |
| 11 | 🟠 **8.7** | `web5-go` · Go | did:web issuer impersonation `CWE-347` | [GHSA-vjhq-pfx7-56h5](https://github.com/decentralized-identity/web5-go/security/advisories/GHSA-vjhq-pfx7-56h5) | 🔄 pending |
| 12 | 🟠 **8.7** | `ssi` (Affinidi) · Dart/pub | JWT-VC issuer impersonation — verifying key bound to the `kid`'s own DID `CWE-347` | [GHSA-ccqw-76rj-rrcq](https://github.com/affinidi/affinidi-ssi-dart/security/advisories/GHSA-ccqw-76rj-rrcq) | 🔄 pending |
| 13 | 🔴 **9.1** | `ueberauth_apple` · Hex/Elixir | "Sign in with Apple" id_token accepted with no `aud`/`iss`/`exp`/`nonce` validation → audience-confusion / replay → ATO `CWE-345` | [GHSA-pxx8-68pc-p9mr](https://github.com/ueberauth/ueberauth_apple/security/advisories/GHSA-pxx8-68pc-p9mr) | ✅ [CVE-2026-55954](https://nvd.nist.gov/vuln/detail/CVE-2026-55954) |
| 14 | 🔴 **9.1** | `Blockthon` · PyPI | Wallet private keys / mnemonics generated with non-CSPRNG Mersenne Twister on the default path → predictable keys `CWE-338` | [GHSA-3xh6-px8p-8mvp](https://github.com/Blockthon/Blockthon/security/advisories/GHSA-3xh6-px8p-8mvp) | 🔄 pending |
| 15 | 🟠 **8.7** | `@hyperledger/identus-sdk` · npm | VP verifier never binds the presenter to the credential subject + no nonce → holder impersonation / presentation replay `CWE-294` | [GHSA-9cv4-xvv9-xg8m](https://github.com/hyperledger-identus/sdk-ts/security/advisories/GHSA-9cv4-xvv9-xg8m) | 🔄 pending |
| 16 | 🟠 **8.7** | `@agledger/verify-core` · npm | Fail-open COSE verify — a 64-byte all-zero signature is accepted as "unsigned" → `valid:true` (even with the high-assurance options) `CWE-347` | [GHSA-8ppx-mwp3-vvmf](https://github.com/agledger-ai/verify-core/security/advisories/GHSA-8ppx-mwp3-vvmf) | 🔄 pending |
| 17 | 🔴 **9.1** | `jwt-bearer-client-auth` · npm | JWT algorithm confusion (RS256→HS256) — asymmetric public key + mixed HS/RS allowlist on jsonwebtoken 8.x → forge client-assertions `CWE-347` | [GHSA-vmwc-xvv7-v2xq](https://github.com/OADA/jwt-bearer-client-auth/security/advisories/GHSA-vmwc-xvv7-v2xq) | 🔄 pending |
| 18 | 🟡 **6.9** | `marqo` · pip/Docker | Unauthenticated SSRF — a search-query string is fetched as a URL gated only by a syntax-only `validators.url` check (accepts loopback / RFC-1918 / `169.254.169.254`); default `0.0.0.0:8882`, no auth → blind internal-network request forgery `CWE-918` | [GHSA-v398-fp89-9j76](https://github.com/marqo-ai/marqo/security/advisories/GHSA-v398-fp89-9j76) | 🔄 pending |
| 19 | 🟠 **7.0** | `encrypt_shared_preferences` · pub.dev | AES-CTR with a constant IV equal to the key for every record → keystream reuse (two-time pad) + unauthenticated ciphertext `CWE-329` | [GHSA-3q27-hwcf-p55w](https://github.com/xaldarof/encrypted-shared-preferences/security/advisories/GHSA-3q27-hwcf-p55w) | 🔄 pending |
| 20 | 🟡 **6.9** | `keechain` · crates.io | Bitcoin BIP39 seed encrypted at rest with an unsalted single-SHA256 password KDF → offline GPU brute-force → seed recovery `CWE-759` | [GHSA-4f56-3j96-qp5w](https://github.com/yukibtc/keechain/security/advisories/GHSA-4f56-3j96-qp5w) | 🔄 pending |
| 21 | 🟠 **8.2** | Identus KMP SDK · Maven (Hyperledger) | VP verifier never verifies the presentation envelope signature → holder identity unauthenticated → present any victim's credential `CWE-347` | [GHSA-2p4v-p249-fqjx](https://github.com/hyperledger-identus/sdk-kmp/security/advisories/GHSA-2p4v-p249-fqjx) | 🔄 pending |
| 22 | 🟠 **7.2** | `unzip-crx` / `unzip-crx-3` · npm | Zip-Slip arbitrary file write on Windows — backslash traversal in CRX entries survives jszip normalization → `path.join` escapes destination → RCE `CWE-22` | [GHSA-hvqj-ph3p-f27f](https://github.com/peerigon/unzip-crx/security/advisories/GHSA-hvqj-ph3p-f27f) | 🔄 pending |
| 23 | 🟠 **8.7** | `@sworddut/mcp-ffmpeg-helper` · npm (MCP) | OS command injection (RCE) — MCP tool arguments (`extraOptions` / `options` / `format` …) are interpolated raw into a `spawn(…, {shell:true})` ffmpeg command string with no escaping or allow-list → arbitrary host command, reachable via MCP indirect prompt injection `CWE-78` | MITRE — CVE pending | 🔄 pending |
| 24 | 🟠 **8.8** | `ssrfcheck` · npm | SSRF-guard bypass via NFKD parser differential — `isSSRFSafeURL()` validates the NFKD-normalized URL, but the app fetches the raw input; fullwidth `＃` / `？` fold the host boundary so the checker approves a URL whose real host is internal (loopback / RFC-1918 / `169.254.169.254`) `CWE-918` | [GHSA-vjf4-72mq-xh5v](https://github.com/felippe-regazio/ssrfcheck/security/advisories/GHSA-vjf4-72mq-xh5v) | 🔄 pending |
| 25 | 🟡 **6.9** | `next-sitemap` · npm | XML injection (sitemap poisoning / content-spoofing) — core `<url>` fields (`loc`/`lastmod`/`changefreq`/`priority`) and `alternateRefs` `href`/`hreflang` are emitted unescaped while news/image/video text fields are escaped, so a dynamic sitemap built from attacker-influenced data can be poisoned with forged `<url>` entries. Served as `application/xml` → no XSS/RCE `CWE-91` | [GHSA-xh82-92vx-jh65](https://github.com/iamvishnusankar/next-sitemap/security/advisories/GHSA-xh82-92vx-jh65) | 🔄 pending |
| 26 | 🟠 **8.8** | `dssrf` · npm | SSRF-guard bypass via NFKC parser differential — `is_url_safe()` validates the NFKC-normalized URL (and rejects userinfo / internal hosts), but the app fetches the raw input; fullwidth `＃` / `？` / `／` fold the delimiters so the checker sees host `example.com` with empty userinfo while a normal HTTP client connects to `127.0.0.1` / RFC-1918 / `169.254.169.254` — defeating the library's own userinfo guard `CWE-918` | [GHSA-xx33-w569-xg7j](https://github.com/HackingRepo/dssrf-js/security/advisories/GHSA-xx33-w569-xg7j) | ⚠️ 1.0.7 unreleased |
| 27 | 🟠 **8.7** | `@blazity/next-image-proxy` · npm | Unauthenticated SSRF / allow-list bypass — the proxy follows 3xx redirects without re-validating the target (an allow-listed origin redirects to an internal host / `169.254.169.254` and the response is streamed back), and matches the allow-list with an unanchored regex `CWE-918` | MITRE — CVE pending | 🔄 pending |
| 28 | 🟠 **8.8** | `private-ip` · npm | SSRF-guard bypass via IPv4-mapped IPv6 — `ipv6_check` matches only the dotted `::ffff:127.0.0.1`, never the hex `::ffff:7f00:1` that WHATWG `new URL()` emits, so the guard approves loopback / cloud-metadata `CWE-918` | MITRE — CVE requested | 🔄 pending |
| 29 | 🟠 **8.3** | `es-toolkit` · npm | Prototype pollution in the `es-toolkit/compat` set-by-path family (`set`/`setWith`/`update`/`updateWith`) — the incomplete-safe-key guard rejects only `__proto__`, so a `constructor.prototype.<x>` path walks to `Object.prototype` and pollutes every object in the realm; re-introduces lodash CVE-2020-8203 in a package pulling ~32.3M downloads/week `CWE-1321` | [GHSA-6fxx-7h6q-4x5f](https://github.com/toss/es-toolkit/security/advisories/GHSA-6fxx-7h6q-4x5f) | 🔄 pending |
| 30 | 🟠 **8.8** | `faraday-restrict-ip-addresses` · RubyGems | SSRF egress-guard bypass — the deny-list is built only from IPv4 CIDRs while the resolver returns IPv6 and `IPAddr#include?` is always false across address families, so every IPv6 destination (`::1`, ULA `fc00::/7`, `::ffff:<v4>` mapped literals incl. cloud metadata) passes `deny_rfc1918`/`deny_rfc6890` `CWE-918` | MITRE — CVE requested | 🔄 pending |
| 31 | 🔴 **9.1** | `jsontokens` · npm | Signature-verification bypass — on the expanded/JWS-JSON token form `verifyExpanded` sets `verified=true` then only clears it inside a loop over the signature array, so an empty `signature:[]` vacuously passes and a fully attacker-controlled token is accepted (reachable when the consumer verifies the object form; the compact-string path is safe) `CWE-347` | MITRE — CVE requested | 🔄 pending |
| 32 | 🟠 **8.6** | `prefect` · pip | Result-store pickle deserialization RCE — a persisted result / background-task-parameter record is loaded with `cloudpickle.loads` and **the stored blob names its own serializer**, so an attacker record declaring `{"type":"pickle"}` overrides a deployment configured for JSON; a lower-trust writer of a shared result / task-param store gets code execution in the reader (a task worker, or a higher-trust flow reading a poisoned cache entry) `CWE-502` | [GHSA-fx6g-c8gr-xhx9](https://github.com/PrefectHQ/prefect/security/advisories/GHSA-fx6g-c8gr-xhx9) | 🔄 pending |
| 33 | 🟡 **6.9** | `dvc` · pip | Arbitrary file write outside the workspace via a malicious `.dvc` inline `outs[].files[].relpath` — `dvc pull`/`checkout`/`import` materialize an attacker-controlled directory file-list, joining each `relpath` onto the output dir with no containment check, so a `../../` entry escapes the workspace (write to an auto-run file → RCE) `CWE-22` | [GHSA-278j-wfpv-rp8f](https://github.com/treeverse/dvc/security/advisories/GHSA-278j-wfpv-rp8f) | 🔄 pending |
| 34 | 🟡 **6.9** | `shiny` (py-shiny) · pip | py-shiny ≤ 1.6.3: unauth bookmark path traversal `CWE-22` | [GHSA-47c3-hpmg-7j6p](https://github.com/posit-dev/py-shiny/security/advisories/GHSA-47c3-hpmg-7j6p) | 🩹 fixed in 1.6.4 |
| 35 | 🟠 **7.1** | `replicate` · pip | replicate ≤ 1.0.7: API token leak to untrusted hosts `CWE-522` | [GHSA-7v25-mxqf-p9c4](https://github.com/replicate/replicate-python/security/advisories/GHSA-7v25-mxqf-p9c4) | 🔄 pending |
| 36 | 🟠 **8.5** | `@agent-infra/mcp-server-filesystem` · npm (MCP) | @agent-infra/mcp-server-filesystem ≤ 1.2.29: jail escape `CWE-22` | [GHSA-c5xr-72g8-4gh8](https://github.com/bytedance/UI-TARS-desktop/security/advisories/GHSA-c5xr-72g8-4gh8) | 🔄 pending |
| 37 | 🟠 **8.7** | `modelscope` · pip | modelscope ≤ 1.38.1: video-pipeline command injection (RCE) `CWE-78` | [GHSA-c69m-g9x8-gc8c](https://github.com/modelscope/modelscope/security/advisories/GHSA-c69m-g9x8-gc8c) | 🔄 pending |
| 38 | 🟠 **8.7** | `go-square` · Go (Celestia) | Reachable panic / denial-of-service via an exported parsing API — availability-only, downstream / public-API scope (details embargoed until fixed) `CWE-129` | [GHSA-fg3q-p289-h9rr](https://github.com/celestiaorg/go-square/security/advisories/GHSA-fg3q-p289-h9rr) | 🔄 pending |
| 39 | 🟠 **8.7** | `@cyanheads/git-mcp-server` · npm (MCP) | Argument injection reachable from MCP tool input, leading to arbitrary file write — details embargoed until fixed `CWE-88` | [GHSA-p9rp-mqwc-4chg](https://github.com/cyanheads/git-mcp-server/security/advisories/GHSA-p9rp-mqwc-4chg) | 🔄 pending |
| 40 | 🟠 **8.6** | `sglang` · pip | Remote code execution on the model-load path when the server runs in a supported optimized mode; same class as vLLM CVE-2026-41523, confirmed against the published wheel — details embargoed until fixed `CWE-94` | [GHSA-pfxh-v2c2-9rx3](https://github.com/sgl-project/sglang/security/advisories/GHSA-pfxh-v2c2-9rx3) | 🔄 pending |
| 41 | 🟠 **8.7** | `dify` · Docker/self-hosted | Unauthenticated access to a console API endpoint that reaches a cloud AI service with the server's own credentials, returning retrieved content to the caller — details embargoed until fixed `CWE-306` | [GHSA-8qqf-22fx-3h6x](https://github.com/langgenius/dify/security/advisories/GHSA-8qqf-22fx-3h6x) | 🔄 pending |
| 42 | 🟠 **7.1** | `ncnn` (Tencent) · C++ | Heap out-of-bounds **write** in `Mat::create()` via allocation-size underflow on a negative dimension `CWE-787` | [GHSA-hr7q-gf7r-jw2f](https://github.com/Tencent/ncnn/security/advisories/GHSA-hr7q-gf7r-jw2f) | 🔄 pending |
| 43 | 🟠 **7.1** | `ncnn` (Tencent) · C++ | Out-of-bounds write — blob indices read from the model file are used as vector subscripts with no bounds or sign check `CWE-787` | [GHSA-hh92-7m77-wx77](https://github.com/Tencent/ncnn/security/advisories/GHSA-hh92-7m77-wx77) | 🔄 pending |
| 44 | 🟠 **8.2** | `picklescan` · pip | Scanner evasion — a code-executing pickle scans CLEAN, defeating the tool's entire purpose `CWE-693` | [GHSA-67cg-2xqg-39qm](https://github.com/mmaitre314/picklescan/security/advisories/GHSA-67cg-2xqg-39qm) | 🔄 pending |
| 45 | 🟡 **6.9** | `lightgbm` · pip | Out-of-bounds read + adjacent-heap disclosure — the `tree_sizes` branch walks the model text unbounded while the sibling branch is bounded `CWE-125` | [GHSA-g64f-8q9j-5g3g](https://github.com/microsoft/LightGBM/security/advisories/GHSA-g64f-8q9j-5g3g) | 🔄 pending |
| 46 | 🟠 **8.5** | `mlrun` · pip | Artifact metadata dictates the deserializer — the artifact stamps `allow_pickle=True` back into a loader whose own docstring says it defaults False "for security reasons" `CWE-502` | [GHSA-8fw9-wp5x-7294](https://github.com/mlrun/mlrun/security/advisories/GHSA-8fw9-wp5x-7294) | 🔄 pending |
| 47 | 🟠 **8.5** | `camel-ai` · pip | No path containment on an LLM-callable file write, while a sibling toolkit does `commonpath` containment by default `CWE-22` | [GHSA-79xf-46xq-6v4x](https://github.com/camel-ai/camel/security/advisories/GHSA-79xf-46xq-6v4x) | 🔄 pending |
| 48 | 🟡 **6.9** | `catboost` · pip | `TreeSplits` values used as unchecked subscripts; the adjacent `CB_ENSURE` validates the dereferenced result rather than the index `CWE-125` | [GHSA-988f-fm5v-rwvv](https://github.com/catboost/catboost/security/advisories/GHSA-988f-fm5v-rwvv) | 🔄 pending |
| 49 | 🟡 **5.3** | `ncnn` (Tencent) · C++ | 16 crash sites reachable from `load_model()` on a crafted model `CWE-20` | [GHSA-2q52-m5cm-grpm](https://github.com/Tencent/ncnn/security/advisories/GHSA-2q52-m5cm-grpm) | 🔄 pending |
| 50 | 🟠 **7.0** | `mergekit` · pip | Bare `torch.load` on an untrusted checkpoint, beside two already-hardened siblings `CWE-502` | [GHSA-3q3r-2gp5-6gxw](https://github.com/arcee-ai/mergekit/security/advisories/GHSA-3q3r-2gp5-6gxw) | 🔄 pending |
| 51 | 🟡 **6.9** | `kserve` · pip/K8s | Storage-initializer path traversal — remote object keys are concatenated onto the download dir with no containment; confirmed inside the shipped `storage-initializer` container `CWE-22` | [GHSA-f8m6-j2c5-mpg9](https://github.com/kserve/kserve/security/advisories/GHSA-f8m6-j2c5-mpg9) | 🔄 pending |
| 52 | 🟡 **6.9** | `mediapipe` · pip | Heap out-of-bounds read in the `.task`/`.tflite` zip reader — the declared `uncompressed_size` is never bounded against the buffer `CWE-125` | [GHSA-cxq2-4ww8-66gg](https://github.com/google-ai-edge/mediapipe/security/advisories/GHSA-cxq2-4ww8-66gg) | 🔄 pending |
| 53 | 🟡 **6.9** | `tflite-support` · pip | Same root cause as the MediaPipe reader and its **origin**; five SIGSEGVs reproduced on the published 0.4.4 wheel via the C++ Task Library `CWE-125` | [GHSA-36rc-j835-7f2p](https://github.com/tensorflow/tflite-support/security/advisories/GHSA-36rc-j835-7f2p) | 🔄 pending |
| 54 | 🟡 **6.9** | LiteRT-LM · C++ (Google) | Same root cause again — the rewrite **moved** the pointer arithmetic into `GetFile()` rather than adding a bound `CWE-125` | [GHSA-m5m7-3892-4qpc](https://github.com/google-ai-edge/LiteRT-LM/security/advisories/GHSA-m5m7-3892-4qpc) | 🔄 pending |
| 55 | 🟢 **2.3** | `pydicom` · pip | `FileSet.write()` hardened the **source** of every file operation and left the destination unchecked → a file moves outside the File-set root via a pre-existing junction `CWE-22` | [GHSA-2rf8-5q2v-f6qg](https://github.com/pydicom/pydicom/security/advisories/GHSA-2rf8-5q2v-f6qg) | 🔄 pending |
| 56 | 🟢 **2.3** | `skops` · pip | `RandomGeneratorNode` constructs a class named by the file — the name is a plain value, so it never reaches `get_untrusted_types()` and the audit reports nothing `CWE-502` | [GHSA-rp88-xr4j-hf3x](https://github.com/skops-dev/skops/security/advisories/GHSA-rp88-xr4j-hf3x) | 🔄 pending |
| 57 | 🟡 **5.3** | `milvus` · Go | Unauthenticated write to a management-port endpoint left open by an earlier remediation that gated its sibling — details embargoed until fixed `CWE-306` | [GHSA-74vw-qgrc-35v7](https://github.com/milvus-io/milvus/security/advisories/GHSA-74vw-qgrc-35v7) | 🔄 pending |
<sub>Reported via GitHub Security Advisory (credit accepted), except rows 23 / 27 / 28 / 30 / 31 (MITRE-routed, no PVR). CVE IDs land on publication. The Sev column is the FIRST.org **CVSS v4.0 Base** score — cross-checked between two independent calculators for rows 1–38, single-source for rows 39+.</sub>

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
