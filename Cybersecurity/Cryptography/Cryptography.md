# First NIST Quantum Standards

NIST began its efforts to test and standardize post-quantum cryptographic systems nearly a decade ago. Their work involved evaluating **82 algorithms** for their resilience against quantum computing attacks. This extensive evaluation process has led to the establishment of finalized standards based on three key algorithms: **ML-KEM** (for general encryption), **ML-DSA** (for digital signatures), and **SLH-DSA** (a backup digital signature method).

## Overview of the Finalized Standards

The three standards are summarized as follows:

### FIPS 203

**Module-Lattice-Based Key-Encapsulation Mechanism (ML-KEM, formerly “CRYSTALS-Kyber”)**

- A key-encapsulation mechanism that enables two parties to establish a shared secret key securely over a public channel.
- Based on the **Module Learning with Errors (MLWE)** problem, it offers strong resistance against quantum attacks.
- The standard includes three parameter sets: **ML-KEM-512**, **ML-KEM-768**, and **ML-KEM-1024** to balance security strength and performance.
- This standard is crucial for ensuring the protection of sensitive U.S. government communication systems in a post-quantum era.

### FIPS 204

**Module-Lattice-Based Digital Signature Algorithm (ML-DSA, formerly “CRYSTALS-Dilithium”)**

- A digital signature algorithm designed to authenticate identities and ensure message integrity.
- Also based on the **MLWE** problem, it provides security against quantum threats.
- Suitable for applications like electronic documents and secure communications.

### FIPS 205

**Stateless Hash-Based Digital Signature Algorithm (SLH-DSA, formerly “Sphincs+”)**

- Specifies a stateless hash-based digital signature algorithm, serving as an alternative to ML-DSA in case ML-DSA proves vulnerable.
- Using a hash-based approach, **SLH-DSA** ensures security against quantum attacks.
- Ideal for scenarios where stateless operations are preferred.

## Adoption and Future Considerations

NIST encourages system administrators to start integrating these new encryption methods immediately, as the transition to quantum-resistant standards will take time.

- **Tech leaders and privacy-focused product vendors**, including Google, Signal, Apple, Tutanota, and Zoom, have already implemented NIST-approved post-quantum encryption standards, like the Kyber key encapsulation algorithm, to protect data in transit.

In addition to these finalized standards, NIST continues to evaluate other algorithms for potential future use as backup standards.

**Confidence in the current selections cannot be absolute**, given that experiments to determine their resilience are practically restricted by the lack of fully-fledged quantum computing systems.

Source: https://www.bleepingcomputer.com/news/security/nist-releases-first-encryption-tools-to-resist-quantum-computing/
