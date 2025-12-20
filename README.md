# Computational Theory
## Project Overview
This project involves the implementation of the [Secure Hash Standard](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf) to develop a function SHA-256 hashing algorithm.

## Problems Solved

### Problem 1: 
Problem 1 focused on implementing the foundational bitwise operations as listed below.
1. `Parity(x, y, z)`
2. `Ch(x, y, z)`
3. `Maj(x, y, z)`
4. `Sigma0(x)` - written as $\Sigma_0^{\{256\}}(x)$ in the standard.
5. `Sigma1(x)` - written as $\Sigma_1^{\{256\}}(x)$ in the standard.
6. `sigma0(x)` - written as $\sigma_0^{\{256\}}(x)$ in the standard.
7. `sigma1(x)` - written as $\sigma_1^{\{256\}}(x)$ in the standard.

**Each operation used exclusively 32-bit integers.**

### Problem 2: SHA-256 Constants Generation
Generates the 64 constant values (K₀ through K₆₃) used in SHA-256 by:
- Computing the first 64 prime numbers
- Taking the cube root of each prime
- Extracting the first 32 bits of the fractional part
- Converting to hexadecimal format

### Problem 3: Message Padding and Block Parsing
Implements the `block_parse(msg)` generator function that prepares messages for SHA-256 processing:
- Appends a '1' bit to mark the end of the message
- Adds zero padding to reach 448 bits (mod 512)
- Appends the original message length as a 64-bit integer
- Yields 512-bit (64-byte) blocks ready for hashing

Handles messages of any length and ensures proper formatting for the hash computation.

### Problem 4: SHA-256 Hash Computation
Implements the core `hash(current, block)` compression function that:
- Expands each 512-bit block into a 64-word message schedule
- Processes 64 rounds of cryptographic operations using Ch, Maj, and Sigma functions
- Mixes the current hash state with the message block
- Produces an updated 256-bit hash value

This is the heart of the SHA-256 algorithm where the actual cryptographic transformation occurs.

### Problem 5: Password Cracking Analysis
Demonstrates the vulnerability of unsalted, single-pass SHA-256 for password storage:
- Successfully cracks three password hashes using dictionary attack
- Tests common passwords and variations against target hashes
- Finds matches by comparing computed hashes with stolen hashes

**Key Findings:**
Passwords cracked in less than a second due to:
- No salt (same password = same hash)
- Single-pass hashing (very fast to compute)
- Common/predictable password choices

**Security Recommendations:**
1. **Salt**: Add unique random data per user
2. **Slow hashing**: Use bcrypt, scrypt, or Argon2 instead of SHA-256
3. **Key stretching**: Apply hash function thousands of times
4. **Pepper**: Include secret server-side key
5. **Strong policies**: Enforce complex passwords and check against breach databases

This demonstrates why SHA-256 alone is inadequate for password storage and why modern systems use specialized password hashing functions.
