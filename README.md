# Modern Cryptography Presentation Series

A collection of detailed, graphical presentations covering the theory, standards, and implementation of modern cryptographic systems — from mathematical foundations through to SoC hardware and software.

## Series Overview

| # | Presentation | Status |
|---|---|---|
| **01** | **Finite Field Arithmetic for Cryptography** | ✅ Complete |
| 02 | Elliptic Curve Cryptography (ECC) | Planned |
| 03 | AES — Design & Implementation | Planned |
| 04 | Hash Functions & MACs | Planned |
| 05 | Public Key Cryptography (RSA, DH) | Planned |
| 06 | Digital Signatures (ECDSA, EdDSA) | Planned |
| 07 | Post-Quantum Cryptography | Planned |
| 08 | Key Exchange Protocols | Planned |
| 09 | Side-Channel Attacks & Countermeasures | Planned |
| 10 | Crypto Hardware Accelerator Design | Planned |

## Presentation 01: Finite Field Arithmetic for Cryptography

**15 slides** covering the complete landscape of finite field arithmetic as used in cryptographic systems.

### Topics Covered

- **Algebraic Foundations** — Groups, rings, fields, and the definition of finite (Galois) fields
- **Prime Fields GF(p)** — Modular arithmetic, the primes behind P-256, Curve25519, P-384, P-521, and Curve448
- **Binary Extension Fields GF(2ⁿ)** — Polynomial arithmetic, irreducible polynomials, XOR-based operations
- **Cryptographic Standards** — Detailed mapping of which fields are used in AES, AES-GCM, NIST ECC curves, Curve25519/448, and SM2, with rationale for each choice
- **Hardware Implementation** — SoC/ASIC, FPGA, and software approaches including composite field decomposition, Montgomery multiplication, systolic arrays, and carry-less multiply
- **SystemVerilog Examples** — Complete RTL for a GF(2⁸) multiplier (Russian peasant algorithm) and parameterized modular add/subtract for GF(p)
- **Python Examples** — Full GF(2⁸) class with multiply and Fermat inverse, and GF(p) class for ECC field arithmetic
- **Performance Analysis** — Throughput comparison chart (SW through 45nm ASIC), trade-off table (area vs. speed vs. side-channel resistance)

### Key Standards Referenced

- FIPS 197 (AES)
- NIST SP 800-186 (Recommendations for Discrete Log-Based and Elliptic Curve Cryptography)
- RFC 7748 (Elliptic Curves for Security — Curve25519, Curve448)
- FIPS 186-4/5 (Digital Signature Standard — P-256, P-384, P-521)

## Directory Structure

```
modern-cryptography-series/
├── README.md
└── 01-finite-field-arithmetic/
    └── finite_field_arithmetic.pptx
```

## How to Use

Each `.pptx` file is a standalone presentation that can be opened in:
- Microsoft PowerPoint (recommended for best rendering)
- LibreOffice Impress
- Google Slides (upload to Google Drive)

The presentations use a consistent dark "Midnight Cipher" visual theme with:
- Georgia headings, Calibri body text, Consolas for code
- Teal/gold/navy color palette designed for readability in both projected and screen viewing
- Embedded icons (no external dependencies)
- Charts rendered natively in PowerPoint

## Technical Notes

- Code examples in the presentations are syntactically correct and functional
- The SystemVerilog GF(2⁸) multiplier synthesizes to ~100-150 gates in typical standard cell libraries
- Python examples use only the standard library (no external dependencies)
- All field parameters match the values in the cited NIST standards

## License

Educational use. Standards references are to publicly available NIST, IETF, and ISO documents.
