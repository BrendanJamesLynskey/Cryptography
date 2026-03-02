# 🔐 Modern Cryptography Presentation Series

Interactive slide decks covering modern cryptographic systems end-to-end — from the underlying mathematics through NIST standards to SystemVerilog RTL and Python implementations.

## ▶ [Open the Series Landing Page](https://OWNER.github.io/REPO/)

> **Setup:** Enable GitHub Pages (Settings → Pages → Deploy from `main` branch, `/ (root)` directory), then replace `OWNER` and `REPO` in the link above with your GitHub username and repository name.
>
> Alternatively, open `index.html` locally in any browser — all presentations work offline after first load.

---

## Presentations

| # | Topic | Slides | Status |
|:-:|-------|:------:|:------:|
| 01 | Finite Field Arithmetic for Cryptography | 16 | ✅ Complete |
| 02 | Elliptic Curve Cryptography (ECC) | — | Planned |
| 03 | AES — Design & Implementation | — | Planned |
| 04 | Hash Functions & MACs | — | Planned |
| 05 | Public Key Cryptography (RSA, DH) | — | Planned |
| 06 | Digital Signatures (ECDSA, EdDSA) | — | Planned |
| 07 | Post-Quantum Cryptography | — | Planned |
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

## Repository Structure

```
├── index.html                         ← Landing page (links to all presentations)
├── README.md                          ← This file
└── 01-finite-field-arithmetic/
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

FIPS 197 (AES) · NIST SP 800-186 (ECC Curves) · RFC 7748 (Curve25519/448) · FIPS 186-5 (DSS) · Canright, "A Very Compact Rijndael S-box" (2005) · Kleppmann, "Implementing Curve25519/X25519" (2020) · Koç et al., "Finite Field Arithmetic for Cryptography," IEEE (2010)

## License

Educational use. Code examples provided as-is. Standards references are to publicly available NIST, IETF, and ISO documents.
