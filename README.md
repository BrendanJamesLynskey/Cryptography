# 🔐 Modern Cryptography Presentation Series

Interactive slide decks covering modern cryptographic systems end-to-end — from the underlying mathematics through NIST standards to SystemVerilog RTL and Python implementations.

## ▶ [Open the Series Landing Page](https://brendanjameslynskey.github.io/Cryptography/)

> **Setup:** Enable GitHub Pages (Settings → Pages → Deploy from `main` branch, `/ (root)` directory), then replace `OWNER` and `REPO` in the link above with your GitHub username and repository name.
>
> Alternatively, open `index.html` locally in any browser — all presentations work offline after first load.

---

## Presentations

| # | Topic | Slides | Status |
| --- | --- | --- | --- |
| 01 | Finite Field Arithmetic for Cryptography | 16 | ✅ Complete |
| 02 | Elliptic Curve Cryptography (ECC) | — | Planned |
| 03 | AES — Design & Implementation | — | Planned |
| 04 | Hash Functions & MACs | — | Planned |
| 05 | Public Key Cryptography (RSA, DH) | — | Planned |
| 06 | Digital Signatures (ECDSA, EdDSA) | — | Planned |
| 07 | Post-Quantum Cryptography | — | Planned |
| 08 | Key Exchange Protocols | — | Planned |
| 09 | Side-Channel Attacks & Countermeasures | — | Planned |
| 10 | Crypto Hardware Accelerator Design | 38 | ✅ Complete |



---

## Presentation 01: Finite Field Arithmetic

16 interactive slides covering:

**Theory** — Group → Ring → Field → Finite Field progression. GF(p) prime fields with GF(7) worked examples. GF(2ⁿ) binary extension fields with AES polynomial arithmetic.

**Standards** — Which fields are used in AES, AES-GCM, NIST P-256, Curve25519, Curve448, and SM2 — and the engineering reasons behind each choice.

**Hardware** — SoC/ASIC composite field decomposition, FPGA LUT and Canright S-box designs, Montgomery multiplication with four architecture variants (bit-serial through full-parallel systolic array).

**Code** — Complete SystemVerilog GF(2⁸) multiplier, parameterized modular add/subtract modules, Python GF(2⁸) and GF(p) classes with Fermat inverse.

**Performance** — Throughput comparison from 3.2 Gbps (OpenSSL) to 53 Gbps (45nm ASIC), with area/speed/side-channel trade-off analysis.

---

## Presentation 10: Crypto Hardware Accelerator Design

38 interactive slides covering:

**Symmetric Engines** — AES round architecture from iterative (2,645 GE, 94 Mbps) to fully pipelined (742 Gbps multi-core FPGA). S-Box implementation via composite field tower decomposition (Canright), Boyar-Peralta logic minimization, and threshold implementation for DPA resistance. AES-GCM authenticated encryption with GF(2¹²⁸) GHASH unit architectures. SHA-3/Keccak hardware achieving 36.4 Gbps on Virtex-7 with unrolled round optimization.

**Asymmetric / PKC Engines** — RSA Montgomery multiplication hardware in four variants: bit-serial, word-serial (DSP48E1), systolic array, and full-parallel. ECC scalar multiplication hierarchy from modular arithmetic through point operations to full scalar multiply. Edwards25519 FPGA implementation with unified point add/double achieving 1.4 ms per operation.

**Post-Quantum Hardware** — NIST PQC standards (FIPS 203/204/205) and their hardware bottlenecks. NTT butterfly architecture deep dive covering Cooley-Tukey and Gentleman-Sande formulations. NTT hardware architectures: iterative, Multi-Delay Commutator (MDC), Single-path Delay Feedback (SDF), and mixed-radix. Unified Kyber+Dilithium accelerators sharing NTT and Keccak datapaths. PQC SoC integration with RISC-V via bus-attached accelerators and instruction set extensions.

**Side-Channel Defense** — Taxonomy of power analysis (SPA/DPA/CPA/HO-DPA), electromagnetic, timing, and fault-injection attacks. Hardware countermeasures: Boolean masking, threshold implementation (TI) with correctness/non-completeness/uniformity properties, dual-rail logic (WDDL), random shuffling, blinding, EM shielding, and voltage/clock monitors. TVLA validation methodology — Rambus DPA-resistant cores validated to 100M+ traces.

**RTL Examples** — Complete SystemVerilog implementations of AES round logic with 16 parallel composite-field S-Boxes, the Canright tower-field S-Box decomposition (GF(2⁸) → GF(((2²)²)²)), NTT Cooley-Tukey butterfly for ML-KEM, and multiplier-less Montgomery reduction exploiting Kyber's q=3329 structure.

**Implementation Platforms** — ASIC vs. FPGA trade-off analysis across performance, area, power, flexibility, and certification. Crypto instruction set extensions (x86 AES-NI, AArch64, RISC-V Zkn/Zks). Protocol-level offload engines for IPsec, MACsec, and TLS. Complete design flow from algorithm analysis through FIPS 140-3 / Common Criteria certification.

**Performance Benchmarks** — Comparative tables spanning AES implementations (2,645 GE to 742 Gbps), PQC NTT accelerators with area-time product improvements up to 82%, and FALCON ASIC achieving 5.2K signatures/sec at 28 nm.

**Future Directions** — Crypto agility for PQC migration, FHE accelerators (FAB: 456× CPU speedup), ZK-proof hardware, and the convergence of NTT as shared IP across PQC/FHE/ZK applications.

---

## Repository Structure

```
├── index.html                                    ← Landing page (links to all presentations)
├── README.md                                     ← This file
├── 01-finite-field-arithmetic/
│   └── index.html                                ← Reveal.js interactive slide deck
└── 10-crypto-hardware-accelerator-design/
    └── index.html                                ← Reveal.js interactive slide deck
```

Each presentation is a single self-contained `index.html`. No build step, no npm — just HTML/CSS/JS with CDN-hosted Reveal.js and Google Fonts.

## Slide Controls

| Action | Key |
| --- | --- |
| Next / Previous | `→` `←` or swipe |
| Overview | `Esc` |
| Fullscreen | `F` |
| Export to PDF | append `?print-pdf` to URL |

## Technology

[Reveal.js 4.6](https://revealjs.com) · [highlight.js](https://highlightjs.org) (Monokai) · Playfair Display + DM Sans + JetBrains Mono

## References

FIPS 197 (AES) · FIPS 202 (SHA-3) · FIPS 203 (ML-KEM) · FIPS 204 (ML-DSA) · FIPS 205 (SLH-DSA) · FIPS 140-3 (Crypto Module Security) · NIST SP 800-186 (ECC Curves) · RFC 7748 (Curve25519/448) · FIPS 186-5 (DSS) · Canright, "A Very Compact Rijndael S-box" (CHES 2005) · Kleppmann, "Implementing Curve25519/X25519" (2020) · Boyar & Peralta, "New Logic Minimization Techniques" (2010) · Kocher, Jaffe & Jun, "Differential Power Analysis" (CRYPTO 1999) · Koç et al., "Finite Field Arithmetic for Cryptography" (IEEE 2010) · Montgomery, "Modular Multiplication Without Trial Division" (1985) · Hasan, "53 Gbps Composite-Field AES" (JSSC 2011) · Ouyang et al., "FalconSign" (TCHES 2025)

## License

Educational use. Code examples provided as-is. Standards references are to publicly available NIST, IETF, and ISO documents.
