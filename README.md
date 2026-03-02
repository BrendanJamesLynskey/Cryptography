# 🔐 Modern Cryptography Presentation Series

A collection of detailed, interactive presentations covering the theory, standards, and implementation of modern cryptographic systems — from mathematical foundations through to SoC hardware and software.

**[🌐 View on GitHub Pages →](https://username.github.io/modern-cryptography-series/)**

> Each presentation is a self-contained HTML slide deck (powered by [Reveal.js](https://revealjs.com)) that runs in any modern browser. No install needed — just open and present.

---

## 📑 Presentations

| # | Topic | Status | View |
|:-:|-------|:------:|------|
| **01** | **[Finite Field Arithmetic for Cryptography](./01-finite-field-arithmetic/)** | ✅ Complete | [Open Presentation](./01-finite-field-arithmetic/) |
| 02 | Elliptic Curve Cryptography (ECC) | 🔜 Planned | — |
| 03 | AES — Design & Implementation | 📋 Planned | — |
| 04 | Hash Functions & MACs | 📋 Planned | — |
| 05 | Public Key Cryptography (RSA, DH) | 📋 Planned | — |
| 06 | Digital Signatures (ECDSA, EdDSA) | 📋 Planned | — |
| 07 | Post-Quantum Cryptography | 📋 Planned | — |
| 08 | Key Exchange Protocols | 📋 Planned | — |
| 09 | Side-Channel Attacks & Countermeasures | 📋 Planned | — |
| 10 | Crypto Hardware Accelerator Design | 📋 Planned | — |

---

## 📖 Presentation 01: Finite Field Arithmetic

**16 interactive slides** covering the complete landscape of finite field arithmetic in cryptography.

### Slide Deck Controls

| Action | Control |
|--------|---------|
| Next slide | `→` or `Space` |
| Previous slide | `←` or `Backspace` |
| Overview mode | `Esc` or `O` |
| Fullscreen | `F` |
| Speaker notes | `S` |
| First/Last slide | `Home` / `End` |

### Topics Covered

**Theory & Foundations**
- Algebraic progression: Group → Ring → Field → Finite Field
- GF(p) prime fields with full GF(7) addition table
- GF(2ⁿ) binary extension fields with worked AES examples
- Key properties: closure, characteristic, irreducible polynomials

**Cryptographic Standards**
- Complete mapping of fields to standards: AES, AES-GCM, P-256, Curve25519, Curve448, SM2
- Detailed rationale for each field choice (why GF(2⁸) for AES, why pseudo-Mersenne primes for ECC)
- NIST SP 800-186, FIPS 197, RFC 7748 references

**Implementation**
- SoC/ASIC: composite field decomposition, AES-NI, systolic arrays
- FPGA: LUT vs. composite field S-box, pipelined architectures, Block RAM tables
- Software: bitsliced, SIMD/AVX2, PCLMULQDQ for GCM, limb arithmetic
- Montgomery multiplication algorithm and four hardware architecture variants

**Code Examples**
- **SystemVerilog**: Complete GF(2⁸) multiplier (Russian peasant algorithm), parameterized modular add/sub
- **Python**: Full GF(2⁸) class with Fermat inverse, GF(p) class for ECC arithmetic

**Performance Analysis**
- Throughput comparison: 3.2 Gbps (OpenSSL) to 53 Gbps (45nm ASIC)
- Trade-off matrix: area vs. speed vs. side-channel resistance

---

## 🚀 Usage

### View Locally

```bash
# Clone the repository
git clone https://github.com/username/modern-cryptography-series.git
cd modern-cryptography-series

# Open any presentation in your browser
open 01-finite-field-arithmetic/index.html
# or
python3 -m http.server 8000
# then visit http://localhost:8000/01-finite-field-arithmetic/
```

### Deploy to GitHub Pages

1. Push to GitHub
2. Go to **Settings → Pages**
3. Set source to **main branch**, root directory
4. Your presentations will be live at `https://username.github.io/modern-cryptography-series/`

### Export to PDF

Open any presentation and append `?print-pdf` to the URL, then use your browser's print function:
```
01-finite-field-arithmetic/index.html?print-pdf
```

---

## 📁 Repository Structure

```
modern-cryptography-series/
├── README.md                          ← This file (series overview)
├── 01-finite-field-arithmetic/
│   └── index.html                     ← Complete interactive presentation
├── 02-elliptic-curve-cryptography/    ← Coming soon
│   └── index.html
├── ...
└── 10-crypto-hw-accelerator-design/
    └── index.html
```

Each presentation is a single `index.html` file with no external dependencies beyond CDN-hosted Reveal.js and Google Fonts. They work offline after first load (assets are cached).

---

## 🔧 Technology

- **[Reveal.js 4.6](https://revealjs.com)** — HTML presentation framework
- **[highlight.js](https://highlightjs.org)** — Syntax highlighting for SystemVerilog and Python
- **[Google Fonts](https://fonts.google.com)** — Playfair Display (headings), DM Sans (body), JetBrains Mono (code)
- **No build step** — pure HTML/CSS/JS, no npm/webpack required

---

## 📚 Key References

- FIPS 197 — Advanced Encryption Standard (AES)
- NIST SP 800-186 — Recommendations for Discrete Log-Based and Elliptic Curve Cryptography
- RFC 7748 — Elliptic Curves for Security (Curve25519, Curve448)
- FIPS 186-5 — Digital Signature Standard (P-256, P-384, P-521)
- D. Canright, "A Very Compact Rijndael S-box" (2005)
- M. Kleppmann, "Implementing Curve25519/X25519: A Tutorial" (2020)
- Ç. K. Koç et al., "Finite Field Arithmetic for Cryptography," IEEE Computer (2010)

---

## 📄 License

Educational use. All code examples are provided as-is for learning purposes. Standards references are to publicly available NIST, IETF, and ISO documents.

---

<p align="center"><em>Contributions, corrections, and suggestions are welcome via issues and pull requests.</em></p>
