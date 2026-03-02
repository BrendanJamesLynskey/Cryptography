# 🔐 Modern Cryptography Presentation Series

Interactive slide decks covering modern cryptographic systems end-to-end — from the underlying mathematics through NIST standards to SystemVerilog RTL and Python implementations.

## ▶ [Open the Series Landing Page](https://brendanjameslynskey.github.io/Cryptography/))

> **Setup:** Enable GitHub Pages (Settings → Pages → Deploy from `main` branch, `/ (root)` directory), then replace `OWNER` and `REPO` in the link above with your GitHub username and repository name.
>
> Alternatively, open `index.html` locally in any browser — all presentations work offline after first load.

---

## Presentations

| # | Topic | Slides | Status |
|---|-------|--------|--------|
| 01 | Finite Field Arithmetic for Cryptography | 16 | ✅ Complete |
| 02 | Elliptic Curve Cryptography (ECC) | — | Planned |
| 03 | AES — Design & Implementation | — | Planned |
| 04 | Hash Functions & MACs | — | Planned |
| 05 | Public Key Cryptography (RSA, DH) | — | Planned |
| 06 | Digital Signatures (ECDSA, EdDSA) | — | Planned |
| 07 | Post-Quantum Cryptography | 21 | ✅ Complete |
| 08 | Key Exchange Protocols | — | Planned |
| 09 | Side-Channel Attacks & Countermeasures | — | Planned |
| 10 | Crypto Hardware Accelerator Design | — | Planned |

---

## Presentation 01: Finite Field Arithmetic

16 interactive slides covering:

**Theory** — Group → Ring → Field → Finite Field progression. GF(p) prime fields with GF(7) worked examples. GF(2ⁿ) binary extension fields with AES polynomial arithmetic.

**Standards** — Which fields are used in AES, AES-GCM, NIST P-256, Curve25519, Curve448, and SM2 — and the engineering reasons behind each choice.

**Hardware** — SoC/ASIC composite field decomposition, FPGA LUT and Canright S-box designs, Montgomery multiplication with four architecture variants (bit-serial through full-parallel systolic array).

**Code** — Complete SystemVerilog GF(2⁸) multiplier, parameterized modular add/subtract modules, Python GF(2⁸) and GF(p) classes with Fermat inverse.

**Performance** — Throughput comparison from 3.2 Gbps (OpenSSL) to 53 Gbps (45nm ASIC), with area/speed/side-channel trade-off analysis.

---

## Presentation 07: Post-Quantum Cryptography

21 interactive slides covering:

**The Quantum Threat** — Shor's algorithm breaking RSA/ECC/DH in polynomial time. Grover's quadratic speedup against symmetric ciphers. The "Harvest Now, Decrypt Later" attack model. CRQC timeline estimates and CNSA 2.0 mandates.

**Lattice Mathematics** — Interactive 2D lattice visualisation with Closest Vector Problem demo. SVP, CVP, SIVP, GapSVP hard problems. Learning With Errors (LWE): search vs. decision variants, worst-case to average-case reductions (Regev 2005). Ring-LWE and Module-LWE structured variants. Interactive noise parameter demo showing why error makes LWE hard.

**NIST PQC Standards (Aug 2024)** — FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), FIPS 205 (SLH-DSA). Upcoming: FIPS 206 (FN-DSA/FALCON), HQC (code-based KEM backup). NIST IR 8547 deprecation timeline (2035).

**ML-KEM Deep Dive** — Module-LWE construction: K-PKE → Fujisaki-Okamoto transform → IND-CCA2. Full protocol flow diagram (Alice/Bob key exchange). NTT butterfly architecture and ℤ₃₃₂₉ arithmetic. Parameter sets: ML-KEM-512/-768/-1024 with key/ciphertext sizes.

**ML-DSA Deep Dive** — Fiat-Shamir with Aborts paradigm (Lyubashevsky). Module-LWE + Module-SIS security basis. Parameter sets and abort loop mechanics.

**SLH-DSA (SPHINCS+)** — Hypertree architecture: WOTS+ → XMSS → FORS layers. 12 parameter sets across SHA-2/SHAKE, small/fast modes. Conservative hash-only security assumptions.

**Interactive Comparisons** — Switchable bar charts comparing public key, secret key, and ciphertext/signature sizes across all PQC and classical algorithms. Performance benchmarks: ML-KEM vs. X25519 vs. RSA-2048; ML-DSA vs. Ed25519.

**Hardware Implementation** — NTT accelerator architecture for SoC/FPGA/ASIC. Barrett reduction in ℤ₃₃₂₉. Keccak/SHAKE co-processors. Cortex-M4, Artix-7, and 28nm ASIC benchmarks.

**Code** — Python NTT implementation in ℤ₃₃₂₉ with bit-reversed twiddle factors. Pedagogical ML-KEM key generation sketch with CBD sampling.

**Migration** — Hybrid TLS 1.3 key exchange (X25519 + ML-KEM-768). Three-phase migration roadmap. Crypto-agility design principles. Algorithm decision matrix.

---

## Repository Structure

```
├── index.html                         ← Landing page (links to all presentations)
├── README.md                          ← This file
├── 01-finite-field-arithmetic/
│   └── index.html                     ← Reveal.js interactive slide deck
└── 07-post-quantum-cryptography/
    └── index.html                     ← Reveal.js interactive slide deck
```

Each presentation is a single self-contained `index.html`. No build step, no npm — just HTML/CSS/JS with CDN-hosted Reveal.js and Google Fonts.

## Slide Controls

| Action | Key |
|--------|-----|
| Next / Previous | `→` `←` or swipe |
| Overview | `Esc` |
| Fullscreen | `F` |
| Export to PDF | append `?print-pdf` to URL |

## Technology

[Reveal.js 4.6](https://revealjs.com) · [highlight.js](https://highlightjs.org) (Monokai) · Playfair Display + DM Sans + JetBrains Mono

## References

**Presentation 01:** FIPS 197 (AES) · NIST SP 800-186 (ECC Curves) · RFC 7748 (Curve25519/448) · FIPS 186-5 (DSS) · Canright, "A Very Compact Rijndael S-box" (2005) · Kleppmann, "Implementing Curve25519/X25519" (2020) · Koç et al., "Finite Field Arithmetic for Cryptography," IEEE (2010)

**Presentation 07:** FIPS 203 (ML-KEM) · FIPS 204 (ML-DSA) · FIPS 205 (SLH-DSA) · NIST IR 8547 (PQC Transition) · SP 800-208 (LMS/XMSS) · Shor, "Polynomial-Time Algorithms for Prime Factorization" (1994) · Regev, "On Lattices, Learning with Errors" (2005) · Lyubashevsky, Peikert, Regev, "On Ideal Lattices and RLWE" (2010) · Bos et al., "CRYSTALS-Kyber" (2018) · Ducas et al., "CRYSTALS-Dilithium" (2018) · Bernstein et al., "The SPHINCS+ Signature Framework" (2019)

## License

Educational use. Code examples provided as-is. Standards references are to publicly available NIST, IETF, and ISO documents.
