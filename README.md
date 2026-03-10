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
| 02 | Elliptic Curve Cryptography (ECC) | 38 | ✅ Complete |
| 03 | AES — Design & Implementation | 28 | ✅ Complete |
| 04 | Hash Functions & MACs | 29 | ✅ Complete |
| 05 | Public Key Cryptography (RSA, DH) | 28 | ✅ Complete |
| 06 | Digital Signatures (ECDSA, EdDSA, Schnorr) | 25 | ✅ Complete |
| 07 | Post-Quantum Cryptography | 21 | ✅ Complete |
| 08 | Fully Homomorphic Encryption (FHE) | 39 | ✅ Complete |
| 09 | Side-Channel Attacks & Countermeasures | 22 | ✅ Complete |
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

## Presentation 02: Elliptic Curve Cryptography

38 interactive slides covering:

**Foundations** — Elliptic curves over ℝ with geometric intuition: the chord-and-tangent group law for point addition and doubling. Algebraic addition formulas with detailed derivation. The point at infinity as identity element. Non-singularity condition and discriminant.

**Curves over Finite Fields** — Transition from ℝ to 𝔽ₚ with Hasse's theorem bounding group order. The Elliptic Curve Discrete Logarithm Problem (ECDLP) and why it provides a trapdoor. Security level analysis: 256-bit curve → 128-bit security via Pollard's ρ.

**Scalar Multiplication** — Binary double-and-add (left-to-right), Non-Adjacent Form (NAF) with density 1/3, windowed w-NAF with precomputation. The Montgomery ladder for constant-time, SPA-resistant computation using x-only differential addition.

**Curve Forms** — Short Weierstrass (y² = x³ + ax + b): NIST P-curves, Jacobian/projective coordinates, a = −3 optimization, incomplete addition formulas and the Renes-Costello-Batina 2016 complete formulas. Montgomery curves (Bv² = u³ + Au² + u): x-only arithmetic, differential addition, Curve25519 and Curve448. Twisted Edwards curves (ax² + y² = 1 + dx²y²): complete addition law when d is non-square, unified add/double, extended coordinates, edwards25519. Birational equivalence maps between all three forms.

**Coordinate Systems** — Six systems compared: affine, projective, Jacobian, extended Edwards, Montgomery x-only, Co-Z. Operation counts (M, S, I) for each. Strategy: projective throughout, single final inversion.

**Standards** — NIST P-256/P-384/P-521, Curve25519/Curve448, edwards25519/edwards448, secp256k1, BrainpoolP256r1. NIST SP 800-186 (2023), FIPS 186-5, RFC 7748, RFC 8032. Curve25519 design rationale: prime shape (2²⁵⁵ − 19), scalar clamping, twist security, minimal A = 486662.

**Protocols** — ECDH key agreement with worked Alice–Bob flow for both X25519 (RFC 7748) and NIST P-256 (with validation requirements). ECDSA signing and verification with full mathematical walkthrough, nonce criticality, and RFC 6979 deterministic variant. EdDSA/Ed25519 (RFC 8032): deterministic Schnorr-type signatures, cofactored verification, comparison table vs ECDSA across 8 properties.

**Attacks & Security** — Eight attack classes: Baby-Step Giant-Step, Pollard's ρ, Pohlig-Hellman (smooth order), MOV/Frey-Rück (low embedding degree), Smart's anomalous attack (#E = p), invalid curve attacks, small subgroup attacks, Shor's quantum algorithm. SafeCurves criteria (Bernstein & Lange). Real-world failures: Sony PS3 nonce reuse (2010), Android Bitcoin wallet RNG (2013), Minerva timing (2019), Dual_EC_DRBG NSA backdoor (2013).

**Hardware** — Three-level accelerator hierarchy (scalar mult → point ops → modular arithmetic → big-integer). Montgomery modular multiplication algorithm and four hardware variants (bit-serial to full-parallel). FPGA results: P-256 from 5.26 ms (Virtex-5) to 0.56 ms (Virtex-7, 23.7k LUTs). ASIC results: unified Curve25519+Curve448 at 28nm (1096 kGE, 0.43 ms), low-power Curve25519 at 65nm (49 kGE). Side-channel countermeasure table: scalar blinding, point blinding, projective coordinate randomization, constant-time operations, fault detection.

**Code** — SystemVerilog Montgomery modular multiplier (parameterized N-bit). Jacobian point addition scheduler with FSM and parallel multiplier scheduling. Python ECDH on a toy curve (y² = x³ + 2x + 3 mod 97) with complete point arithmetic.

**Interactive** — Canvas-based point visualizer for E(𝔽₉₇) with click-to-select addition and doubling. Scalar multiplication kG slider showing trail of intermediate points with binary decomposition. Animated group law illustration cycling through addition, doubling, and inversion. All 100 curve points enumerated.

**Deployment** — ECC in TLS 1.3 (X25519 key exchange + Ed25519 signatures), SSH, Bitcoin/Ethereum (secp256k1), Signal/WhatsApp, WireGuard, FIDO2/Passkeys, Tor, smart cards, IoT. ECC vs RSA performance comparison at 128-bit security. Quantum threat: Shor's algorithm resource estimates, CNSA 2.0 timeline, hybrid X25519+ML-KEM-768 transition.

---

## Presentation 03: AES — Design & Implementation

28 interactive slides covering:

**Theory** — GF(2⁸) arithmetic recap with xtime(). S-box two-step construction (multiplicative inverse + affine transformation over GF(2)). Complete 16×16 S-box lookup table. ShiftRows with visual before/after state grids. MixColumns MDS matrix with branch number = 5 analysis. AddRoundKey.

**Standards** — Historical context from DES through the AES competition to FIPS 197. Key schedule for all three variants (128/192/256-bit) with RotWord, SubWord, and Rcon. Round structure pseudocode. Decryption via equivalent inverse cipher.

**Hardware Architectures** — Four AES round implementations compared: iterative (2,645 GE, 1 round/clock), loop-unrolled (3× speed), fully pipelined (1 block/clock), and multi-core parallel (742 Gbps on FPGA). T-box optimization for software. AES-NI x86 instruction set and ARM AES extensions. FPGA-specific techniques: BRAM S-box, distributed LUT S-box, DSP-free round function.

**Modes of Operation** — ECB, CBC, CTR, GCM, CCM, XTS with security properties and IV handling. AES-GCM authenticated encryption: GHASH over GF(2¹²⁸), hardware GHASH unit architectures (4-way Karatsuba), NIST SP 800-38D requirements.

**Side-Channel Countermeasures** — Power analysis classification (SPA, DPA, CPA), cache-timing attacks (Bernstein 2005, OpenSSL vulnerability), Boolean masking theory and hardware masking, threshold implementation (TI) for first-order resistance, random delay insertion, dual-rail logic.

**Key Schedule Security** — Related-key attacks on AES-256 (Biryukov-Khovratovich 2009), biclique attack (Bogdanov et al. 2011) bringing 2¹²⁶·² complexity — best known attack, still impractical.

**Code** — Complete SystemVerilog AES-128 round with 16 parallel composite-field S-boxes (Canright tower-field decomposition). Python AES-ECB implementation from primitives. AES-GCM Python with GHASH.

**Performance** — Throughput from OpenSSL software (3.2 Gbps) to AES-NI (25–53 Gbps on modern CPUs) to custom ASIC (53 Gbps, Mathew et al. JSSC 2011).

---

## Presentation 04: Hash Functions & MACs

29 interactive slides covering:

**Foundations** — Hash function definition, security properties (preimage resistance, second-preimage resistance, collision resistance), birthday bound O(2^(n/2)). Merkle-Damgård construction with compression function chaining, length padding, and why it enables length extension attacks.

**SHA-2** — SHA-256/384/512/512-256 family. Compression function internals: eight working registers (a–h), Ch(e,f,g), Maj(a,b,c), Σ₀(a), Σ₁(e), round constants K_t from cube roots of primes. Message schedule W_t expansion with σ₀/σ₁ rotation functions. Davies-Meyer feedforward. Performance: software throughput, SHA-NI/ARM CE extensions, FPGA/ASIC implementations, Bitcoin mining ASICs.

**Legacy** — MD5 (Wang et al. 2004 collision), SHA-1 (theoretical 2005, SHAttered 2017, SHA-mbles 2020). Deprecation timelines and real-world impact (rogue CA certificates, Flame malware).

**SHA-3 / Keccak** — NIST competition (2007–2012), sponge construction (absorb/squeeze, rate r vs capacity c, security = c/2). Keccak-f[1600] permutation: θ, ρ, π, χ, ι steps over 5×5×64 state. SHA3-224/256/384/512, SHAKE128/256 XOFs, cSHAKE, TupleHash, ParallelHash, KangarooTwelve.

**MACs** — HMAC (Bellare-Canetti-Krawczyk 1996): nested hashing construction and security proof. KMAC (SHA-3 native, no nesting needed). CMAC (cipher-based). Poly1305 (Bernstein). GMAC.

**Applications** — Hash-based signatures (Lamport, WOTS+, XMSS, LMS, SLH-DSA). Merkle trees (proof of inclusion, Git, blockchain, certificate transparency). Password hashing (bcrypt, scrypt, Argon2id). Hash functions in TLS 1.3 (HKDF, transcript hashing).

**Hardware** — SHA-256 round architectures (iterative, unrolled, pipelined). Keccak lane-complementing and bit-interleaving optimizations. FPGA throughput results.

**Code** — SystemVerilog SHA-256 compression round module. Python SHA-256 single-block implementation from scratch. Interactive hash visualizer with live avalanche demonstration via Web Crypto API.

---

## Presentation 05: Public Key Cryptography (RSA, DH)

28 interactive slides covering:

**Foundations** — The key distribution problem (N(N-1)/2 scaling). Number theory: modular arithmetic, Euler's totient φ(n), Fermat's little theorem, Euler's theorem, Chinese Remainder Theorem. Prime number generation and Miller-Rabin primality testing.

**Diffie-Hellman** — Original 1976 protocol: agree on (p, g), exchange g^a mod p and g^b mod p, derive shared secret g^(ab) mod p. Computational Diffie-Hellman (CDH) and Decisional Diffie-Hellman (DDH) assumptions. DLP algorithm hierarchy: baby-step giant-step, Pollard's rho, index calculus, number field sieve. Practical group selection: RFC 3526/7919 MODP groups, ephemeral DH (DHE) for forward secrecy, FFDHE in TLS 1.3.

**RSA** — Key generation (p, q, n=pq, e=65537, d=e⁻¹ mod φ(n)). Encryption c=m^e mod n, decryption m=c^d mod n. Signatures (hash-then-sign). Padding: PKCS#1 v1.5 and Bleichenbacher's 1998 attack, OAEP, PSS. Integer factorization algorithms through GNFS. RSA-768/RSA-250 factoring records. CRT optimization (4× speedup). Multi-prime RSA. Key size recommendations (2048-bit minimum, 3072-bit for longevity).

**Attacks** — RSA: Wiener (small d), Coppersmith (small e), Håstad broadcast, common modulus, timing (Kocher 1996), CRT fault (Boneh-DeMillo-Lipton). DH: MITM, small subgroup, Logjam (2015 precomputation on 512-bit). Why authentication is essential.

**ElGamal & Hybrid Encryption** — ElGamal encryption from DH assumption. KEM/DEM paradigm for bulk encryption. RSA-KEM. HPKE (RFC 9180).

**Infrastructure** — X.509 certificates, certificate chains, CRL/OCSP, Certificate Transparency. RSA vs ECC performance comparison. Forward secrecy (DHE/ECDHE). Quantum threat: Shor's algorithm, qubit estimates, CNSA 2.0 migration timeline.

**Hardware** — Montgomery multiplier architectures (bit-serial to full-parallel). CRT acceleration. FPGA/ASIC implementations. Side-channel countermeasures (blinding, constant-time).

**Code** — SystemVerilog parameterized radix-2 Montgomery modular multiplier. Python RSA key generation with Miller-Rabin, encrypt/decrypt from scratch. Interactive RSA demo with user-selectable small primes.

---

## Presentation 06: Digital Signatures

25 interactive slides covering:

**ECDSA** — Signature generation and verification with full mathematical walkthrough. Nonce (k) criticality: reuse → full key recovery (Sony PS3 2010, Android Bitcoin 2013). RFC 6979 deterministic nonce derivation from HMAC-DRBG.

**EdDSA / Ed25519** — Twisted Edwards curve (-x² + y² = 1 - (121665/121666)x²y²) over 𝔽_(2²⁵⁵-19). Deterministic signing via SHA-512(sk). Cofactor handling. Comparison vs ECDSA across 8 engineering properties. Batch verification speedup.

**Schnorr Signatures** — Linear structure enabling provable security (random oracle model), natural multi-signature support. BIP 340 (Taproot). Comparison with ECDSA.

**Threshold & Multi-Signature** — MuSig2: 2-round multi-signature for Bitcoin Taproot. FROST: flexible round-optimal Schnorr threshold signatures for t-of-n. Comparison of interactivity, communication rounds, and security models.

**Post-Quantum** — ML-DSA (FIPS 204, Dilithium): lattice-based signature with NTT polynomial operations. SLH-DSA (FIPS 205, SPHINCS+): hash-based stateless signatures with FORS + HT construction. Size comparison: Ed25519 (64B sig) vs ML-DSA-65 (3293B) vs SLH-DSA-128s (7856B).

---

## Presentation 07: Post-Quantum Cryptography

21 interactive slides covering:

**Quantum threat** — Shor's algorithm factoring and discrete log in polynomial time. Grover's algorithm halving symmetric key lengths. NIST PQC timeline (2016–2024) and CNSA 2.0 migration schedule.

**Lattice foundations** — Shortest Vector Problem (SVP), Learning With Errors (LWE), Ring-LWE. Why lattice problems resist quantum algorithms.

**ML-KEM (FIPS 203)** — Kyber KEM: key generation, encapsulation, decapsulation. NTT polynomial multiplication in ℤq[x]/(x²⁵⁶+1), q=3329. Module structure (k=2/3/4 for ML-KEM-512/768/1024). IND-CCA2 security via Fujisaki-Okamoto transform.

**ML-DSA (FIPS 204)** — Dilithium signature: commitment, challenge, response. Rejection sampling for security. Module lattice structure. Parameter sets.

**SPHINCS+ / SLH-DSA (FIPS 205)** — Hash-based signatures with no lattice assumptions. FORS few-time signatures + hypertree structure. Stateless, conservative security.

**NTT deep dive** — Cooley-Tukey butterfly in negacyclic ring. SystemVerilog NTT core for ML-KEM. Hardware sharing with AES-SHA-3.

**Hybrid schemes** — X25519+ML-KEM-768, ECDSA+ML-DSA in TLS 1.3 and SSH. NIST IR 8547 transition guidance.

---

## Presentation 08: Fully Homomorphic Encryption

39 interactive slides covering:

**Vision** — The "holy grail" of cryptography: compute on encrypted data without decrypting. FHE vs traditional cloud (plaintext exposure) and the homomorphic property Enc(x) ⊕ Enc(y) = Enc(x+y), Enc(x) ⊗ Enc(y) = Enc(x·y).

**Taxonomy** — PHE (partially: + or × only), SHE (somewhat: bounded depth), LHE (levelled: fixed depth, no bootstrapping), FHE (fully: unlimited depth via bootstrapping). Why multiplicative depth is the critical resource.

**Mathematical Foundations** — LWE: samples b = a·s + e mod q, hardness reduction from GapSVP/SIVP (Regev 2005). Ring-LWE: polynomial ring R = ℤ[x]/(xⁿ+1), RLWE hardness (Lyubashevsky-Peikert-Regev 2010). NTT-friendly cyclotomic structure. Standard parameter tables (n, log₂q) for 128-bit security. Noise growth: linear for addition, multiplicative for multiplication; decryption bound |noise| < q/2.

**Noise management** — Modulus switching (drop a modulus level), key switching (relinearisation), rescaling (CKKS), and bootstrapping (homomorphic decryption to reset noise).

**Schemes** — Gentry's blueprint (2009): self-referential bootstrapping, squashing trick. BGV (2011): modulus switching, RNS chain, levelled FHE. BFV (2012): scale-invariant noise, single large q; BGV vs BFV selection guide. CKKS (2017): approximate arithmetic, scaling factor Δ, n/2 SIMD slots via Galois automorphisms; best for ML/statistics. FHEW (2015): fast bootstrapping <100ms, ring-GSW external product. TFHE (2016/2020): torus LWE, gate-level FHE with programmable bootstrapping <10ms; TFHE vs CKKS comparison table. GSW external product and blind rotation for FHEW/TFHE.

**Bootstrapping deep dive** — CKKS: CoeffToSlot → EvalMod (Chebyshev sine approximation) → SlotToCoeff. Cost table vs n and slot count. Amortised cost per slot enabling practical encrypted ML. TFHE: blind rotation algorithm step-by-step with RGSW accumulators.

**Key operations** — Relinearisation: degree-2 ciphertext reduction using rlk = Enc(s²). Key switching: cross-key reencryption using ksk. Galois rotations for SIMD slot permutation. RNS representation: q = q₀·q₁·…·q_{L-1} (60-bit primes, 64-bit arithmetic). NTT: O(n log n) polynomial multiply; shared IP across FHE, PQC, ZK-SNARKs.

**FHE Libraries** — Microsoft SEAL (BFV, CKKS), OpenFHE (all schemes), HElib (BGV, CKKS), HEAAN (CKKS reference), Concrete/Zama (TFHE, Rust+Python), Lattigo (Go, multiparty). HE-Std HomomorphicEncryption.org white paper: API standards and security parameter tables.

**Compiler toolchain** — Circuit extraction, scheme selection, parameter synthesis, operator scheduling, SIMD packing. HEIR (Google, MLIR-based, 2024), Concrete (Zama), EVA (Microsoft), HECO, Cingulata.

**Hardware Acceleration** — GPU: NTT and RNS limbs are embarrassingly parallel; cuFHE, PhantomFHE (25× SEAL CPU), A100 benchmarks (CKKS HomMul: 0.4ms, Bootstrap: 50ms). FPGA: custom Barrett modular multipliers, pipelined NTT butterflies, Alveo/Stratix 10 results (HEAX ISCA 2020, CraterLake ISCA 2022, FAB ISCA 2022). ASIC: F1 (MIT, MICRO 2021; 5400× CPU speedup), BTS (SNU, ISSCC 2022; on-chip CKKS bootstrapping), Poseidon (ETH 2023; TFHE <1ms gate-boot), Intel HERACLES. Memory bandwidth as the fundamental bottleneck; on-chip SRAM hierarchy design.

**SystemVerilog** — Fully pipelined 3-stage NTT Cooley-Tukey butterfly with 64-bit Barrett modular reduction, parameterised for any NTT-friendly prime.

**Code** — Python CKKS encrypted dot product using Microsoft SEAL bindings: parameter selection, RNS chain configuration, encode/encrypt, HomMul + relinearise + rescale, slot rotation for inner product, decrypt.

**Interactive Scheme Selector** — Questionnaire (plaintext type × circuit depth × priority) → recommended scheme with rationale.

**Applications** — Private ML inference: CKKS NN mapping (polynomial ReLU approximation via Chebyshev, batched linear layers via slot rotations). Published results: LeNet-5 (2s CPU), ResNet-20 (6min CPU / 30s A100), 1-layer BERT hybrid. CryptoNets, nGraph-HE, Concrete ML. Private genomics: GWAS χ² over BGV, PRS inner product (CKKS), iDASH 2021 winner. Regulated finance: private credit scoring (CKKS logistic regression), dark pool matching (TFHE comparison), risk aggregation (Duality). Private database queries: PIR, encrypted SQL aggregates, Spiral protocol.

**Multi-party & ZK** — Threshold FHE: split secret key (Shamir), t-of-n decryption, Lattigo multiparty. FHE + ZK proofs: verifiable FHE (vFHE), SNARK-based correctness proofs, shared NTT datapath with PLONK/Groth16. Applications: private federated learning, auditable encrypted databases, FHE blockchains (fhEVM).

**Security** — IND-CPA security; NOT IND-CCA2 (ciphertext malleability inherent). CKKS approximate leakage (Li-Micciancio 2021): smudging noise and noise flooding countermeasures. Quantum resistance: RLWE hardness not broken by Shor/Grover.

**Standardisation** — HE-Std (HomomorphicEncryption.org): API standard and 128/192/256-bit parameter sets. ISO/IEC 18033-6 (PHE). NIST IR 8481 FHE survey (2023). lattice-estimator (Albrecht et al.) for concrete security estimation.

**Limitations & open problems** — No native comparison/branching (polynomial approximations required), large ciphertext expansion (50–200 KB per float), evaluation key sizes (tens of GB), parameter tuning complexity. Open research: sub-ms CKKS bootstrapping, transciphering, FHE-native NN training, multiparty FHE at scale, functional encryption.

**Ecosystem (2025)** — Commercial: Zama, Duality Technologies, Cornami, Microsoft, Intel, IBM. Research: MIT CSAIL, Stanford, Seoul Nat'l Univ, EPFL, ETH Zürich. Standards: HomomorphicEncryption.org, FHE.org, OpenFHE board.

---

## Presentation 09: Side-Channel Attacks & Countermeasures

22 interactive slides covering:

**Attack taxonomy** — Physical side-channels vs logical. Timing attacks (Kocher 1996): RSA/DH modular exponentiation timing; cache-timing (Bernstein AES 2005, Spectre 2018, Meltdown 2018). Power analysis: SPA (single trace), DPA (Kocher-Jaffe-Jun 1999), CPA (correlation with Hamming weight/distance), template attacks (Chari-Rao-Rohatgi CHES 2002). Electromagnetic attacks: near-field EM probes, EM-DPA. Fault injection: clock/voltage glitching, laser fault injection; Bellcore attack on RSA-CRT (Boneh-DeMillo-Lipton 1997), Piret-Quisquater AES DFA (2003), safe-error attacks.

**Hardware countermeasures** — Boolean masking (ISW private circuits 2003): t-probing security, correctness/uniformity requirements, masked S-box. Threshold Implementation (Nikova-Rechberger-Rijmen 2006): three key properties (correctness, non-completeness, uniformity), first-order DPA resistance. Dual-rail logic (WDDL): balanced power consumption. Random delay insertion and shuffling. Blinding for RSA/ECC. Voltage and clock monitors for fault detection.

**TVLA validation** — Test Vector Leakage Assessment (Goodwill et al. 2011): Welch's t-test on fixed vs random traces; threshold |t| > 4.5 indicates leakage. Rambus DPA-resistant cores validated to 100M+ traces.

**Cache attacks** — Flush+Reload, Prime+Probe, Evict+Time on shared L3 cache. Real-world: OpenSSL AES-128 key recovery in minutes on co-tenant VM. Mitigations: constant-time implementations, cache partition (ARM PA-Range).

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
├── index.html                                      ← Landing page (links to all presentations)
├── README.md                                       ← This file
├── 01-finite-field-arithmetic/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 02-elliptic-curve-cryptography/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 03-aes-design-implementation/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 04-hash-functions-macs/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 05-public-key-cryptography/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 06-digital-signatures/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 07-post-quantum-cryptography/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 08-fully-homomorphic-encryption/
│   └── index.html                                  ← Reveal.js interactive slide deck
├── 09-side-channel-attacks/
│   └── index.html                                  ← Reveal.js interactive slide deck
└── 10-crypto-hardware-accelerator-design/
    └── index.html                                  ← Reveal.js interactive slide deck
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

**Presentation 01:** FIPS 197 (AES) · NIST SP 800-186 (ECC Curves) · RFC 7748 (Curve25519/448) · FIPS 186-5 (DSS) · Canright, "A Very Compact Rijndael S-box" (2005) · Kleppmann, "Implementing Curve25519/X25519" (2020) · Koç et al., "Finite Field Arithmetic for Cryptography," IEEE (2010)

**Presentation 02:** FIPS 186-5 (DSS) · NIST SP 800-186 (ECC Curves, 2023) · RFC 7748 (X25519/X448) · RFC 8032 (EdDSA) · RFC 6979 (Deterministic ECDSA) · SEC 2 (SECG Curves) · RFC 5639 (Brainpool) · Koblitz, "Elliptic Curve Cryptosystems" (1987) · Miller, "Use of Elliptic Curves in Cryptography" (CRYPTO 1985) · Montgomery, "Speeding the Pollard and EC Methods of Factorization" (1987) · Edwards, "A Normal Form for Elliptic Curves" (2007) · Bernstein, "Curve25519: New Diffie-Hellman Speed Records" (2006) · Bernstein & Lange, "Faster Addition and Doubling on Elliptic Curves" (ASIACRYPT 2007) · Renes, Costello, Batina, "Complete Addition Formulas for Prime Order Elliptic Curves" (2016) · Bernstein & Lange, "Montgomery Curves and the Montgomery Ladder" (2017) · Hankerson, Menezes, Vanstone, "Guide to Elliptic Curve Cryptography" (Springer, 2004) · Pohlig & Hellman (1978) · Pollard, "Monte Carlo Methods for Index Computation" (1978) · Smart, "The Discrete Logarithm Problem on Elliptic Curves of Trace One" (1999) · Menezes, Okamoto, Vanstone, "Reducing ECDLP to DLP over Extension Fields" (1993)

**Presentation 03:** FIPS 197 (AES) · Daemen & Rijmen, "The Design of Rijndael" (Springer, 2002) · Canright, "A Very Compact Rijndael S-box" (CHES 2005) · Mathew et al., "53 Gbps AES in 45nm" IEEE JSSC (2011) · Bogdanov et al., "Biclique Cryptanalysis of AES" (ASIACRYPT 2011) · Biryukov & Khovratovich, "Related-Key Attacks on AES-256" (CRYPTO 2009) · Bernstein, "Cache-Timing Attacks on AES" (2005) · Kocher, Jaffe & Jun, "Differential Power Analysis" (CRYPTO 1999) · Gaj & Chodowiec, "FPGA and ASIC Implementations of AES" (2009) · NIST SP 800-38A (Modes of Operation) · NIST SP 800-38D (GCM) · Intel AES-NI White Paper (2010)

**Presentation 04:** FIPS 180-4 (SHA-2) · FIPS 202 (SHA-3) · NIST SP 800-185 (SHA-3 Derived Functions) · RFC 2104 (HMAC) · NIST SP 800-208 (LMS/XMSS) · FIPS 205 (SLH-DSA) · Wang et al., "Collisions for Hash Functions MD4, MD5, HAVAL-128, RIPEMD" (2004) · Stevens et al., "The First Collision for Full SHA-1" (SHAttered, 2017) · Bertoni, Daemen, Peeters, Van Assche, "Keccak Reference" (2011) · Bellare, Canetti, Krawczyk, "Keying Hash Functions for Message Authentication" (CRYPTO 1996) · Bernstein, "The Poly1305-AES Message-Authentication Code" (2005) · Biham & Chen, "Near-Collisions of SHA-0" (CRYPTO 2004) · RFC 9180 (HPKE) · NIST SP 800-132 (PBKDF) · Percival, "Stronger Key Derivation via Sequential Memory-Hard Functions" (scrypt, 2009) · Biryukov, Dinu, Khovratovich, "Argon2" (2015)

**Presentation 05:** Diffie & Hellman, "New Directions in Cryptography" (1976) · Rivest, Shamir, Adleman, "A Method for Obtaining Digital Signatures and Public-Key Cryptosystems" (1978) · FIPS 186-5 (DSS) · RFC 8017 (PKCS#1 v2.2) · RFC 3526/7919 (MODP Groups) · RFC 9180 (HPKE) · Montgomery, "Modular Multiplication Without Trial Division" (1985) · Bleichenbacher, "Chosen Ciphertext Attacks Against Protocols Based on RSA PKCS#1" (CRYPTO 1998) · Adrian et al., "Imperfect Forward Secrecy: How Diffie-Hellman Fails in Practice" (Logjam, 2015) · Wiener, "Cryptanalysis of Short RSA Secret Exponents" (1990) · Coppersmith, "Small Solutions to Polynomial Equations, and Low Exponent RSA Vulnerabilities" (1997) · Boneh, DeMillo, Lipton, "On the Importance of Checking Cryptographic Protocols for Faults" (1997) · Lenstra et al., "Factoring RSA-250" (2020)

**Presentation 06:** FIPS 186-5 (DSS) · FIPS 204 (ML-DSA) · FIPS 205 (SLH-DSA) · NIST SP 800-186 (ECC Curves) · RFC 6979 (Deterministic ECDSA) · RFC 8032 (EdDSA) · BIP 340 (Schnorr) · Johnson, Menezes, Vanstone, "The ECDSA" (2001) · Bernstein et al., "High-speed high-security signatures" (2011)

**Presentation 07:** FIPS 203 (ML-KEM) · FIPS 204 (ML-DSA) · FIPS 205 (SLH-DSA) · NIST IR 8547 (PQC Transition) · SP 800-208 (LMS/XMSS) · Shor, "Polynomial-Time Algorithms for Prime Factorization" (1994) · Regev, "On Lattices, Learning with Errors" (2005) · Lyubashevsky, Peikert, Regev, "On Ideal Lattices and RLWE" (2010) · Bos et al., "CRYSTALS-Kyber" (2018) · Ducas et al., "CRYSTALS-Dilithium" (2018) · Bernstein et al., "The SPHINCS+ Signature Framework" (2019)

**Presentation 08:** Gentry, "A Fully Homomorphic Encryption Scheme," Stanford PhD (2009) · Regev, "On Lattices, LWE, Random Linear Codes," STOC (2005) · Lyubashevsky, Peikert, Regev, "On Ideal Lattices and RLWE," EUROCRYPT (2010) · Brakerski, Gentry, Vaikuntanathan (BGV), ITCS (2012) · Fan, Vercauteren (BFV) (2012) · Cheon, Kim, Kim, Song (CKKS), ASIACRYPT (2017) · Ducas, Micciancio (FHEW), EUROCRYPT (2015) · Chillotti et al. (TFHE), J.Cryptology (2020) · Gentry, Sahai, Waters (GSW), CRYPTO (2013) · Li, Micciancio, "On the Security of HE on Approximate Numbers," EUROCRYPT (2021) · Han, Ki, "Better Bootstrapping for CKKS," CT-RSA (2020) · Reagen et al. (F1), MICRO (2021) · Kim et al. (BTS), ISSCC (2022) · Samardzic et al. (CraterLake), ISCA (2022) · Agrawal et al. (FAB), ISCA (2022) · Boura et al. (HEAX), ISCA (2020) · Viand et al. (Poseidon), ETH (2023) · HE-Std White Paper, HomomorphicEncryption.org (2021) · NIST IR 8481 (2023) · Albrecht et al., "Estimate all the {LWE, NTRU} schemes!", SCN (2018)

**Presentation 09:** Kocher, "Timing Attacks on Implementations of DH, RSA, DSS" (1996) · Kocher, Jaffe & Jun, "Differential Power Analysis" (CRYPTO 1999) · Chari, Rao & Rohatgi, "Template Attacks" (CHES 2002) · Biham & Shamir, "Differential Fault Analysis" (1997) · Boneh, DeMillo & Lipton, "On the Importance of Checking Cryptographic Protocols for Faults" (1997) · Piret & Quisquater, "A DFA Technique Against SPN Structures" (2003) · Bernstein, "Cache-Timing Attacks on AES" (2005) · Kocher et al., "Spectre Attacks" (2018) · Lipp et al., "Meltdown" (2018) · Nikova, Rechberger & Rijmen, "Threshold Implementations" (2006) · ISW, "Private Circuits: Securing Hardware Against Probing Attacks" (2003) · Das & Sen, "EM and Power SCA: Advanced Attacks and Low-Overhead Countermeasures" (2020) · Schneider, Moradi & Güneysu, "Arithmetic Addition over Boolean Masking" (2015) · Goodwill et al., "TVLA — A Testing Methodology for SCA Resistance" (2011) · NIST SP 800-90B · FIPS 140-3 · Common Criteria ISO/IEC 15408

**Presentation 10:** FIPS 197 (AES) · FIPS 202 (SHA-3) · FIPS 203 (ML-KEM) · FIPS 204 (ML-DSA) · FIPS 205 (SLH-DSA) · FIPS 140-3 (Crypto Module Security) · Canright, "A Very Compact Rijndael S-box" (CHES 2005) · Boyar & Peralta, "New Logic Minimization Techniques" (2010) · Kocher, Jaffe & Jun, "Differential Power Analysis" (CRYPTO 1999) · Montgomery, "Modular Multiplication Without Trial Division" (1985) · Hasan, "53 Gbps Composite-Field AES" (JSSC 2011) · Ouyang et al., "FalconSign" (TCHES 2025)

## License

Educational use. Code examples provided as-is. Standards references are to publicly available NIST, IETF, and ISO documents.
