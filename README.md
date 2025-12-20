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

## Getting Started

### Prerequisites
- Python 3.x
- NumPy library
- Jupyter Notebook or VS Code with Jupyter extension

### Installation and Setup

1. **Clone the repository**
```bash
   git clone https://github.com/JosephShortt/compTheoryRepo
   cd compTheoryRepo
```

2. **Install NumPy**
```bash
   pip install numpy
```

3. **Open the notebook**
   - Open the folder in VS Code
   - Install the "Jupyter" extension if you haven't already
   - Open `notebook.ipynb`
   - Click "Run All" or run cells individually with the execute button

### Running the Code

1. **Run cells in order**: The notebook must be executed sequentially as later problems depend on functions from earlier problems.

2. **Execute all cells**: In VS Code or Jupyter, use "Run All" to execute the entire notebook at once.

3. **Individual execution**: You can run specific problems by executing their respective cells using the play button (▶️) next to each cell.

### Expected Output
- **Problem 2**: List of 64 hexadecimal constants
- **Problem 3**: Padded message blocks in hexadecimal
- **Problem 4**: SHA-256 hash output for test cases
- **Problem 5**: Cracked passwords and security analysis

### Testing
To verify the implementation works correctly, check that:
- The hash of "abc" produces: `ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad`
- All three passwords in Problem 5 are successfully cracked


## Conclusion

This project demonstrates a complete implementation of the SHA-256 cryptographic hash algorithm 

### Key Takeaways

**Technical Understanding:**
- SHA-256 is built on simple bitwise operations (XOR, AND, rotations) that combine to create cryptographic security
- The algorithm's constants are derived transparently from prime numbers, ensuring no hidden backdoors
- Padding and block processing enable consistent handling of variable-length inputs
- The 64-round compression function creates the avalanche effect where small input changes produce dramatically different outputs

**Security Lessons:**
The password cracking exercise revealed critical vulnerabilities in naive password storage:
- **Speed is the enemy**: SHA-256's efficiency (designed for data integrity) makes it terrible for passwords
- **Predictability is fatal**: Even "complex" passwords like `P@ssw0rd` are easily cracked if they follow common patterns
- **Defense in depth matters**: Proper password security requires multiple layers (salt + slow hashing + strong policies)


By building SHA-256 from scratch and exploiting its weaknesses in password storage, this project bridges the gap between theoretical cryptography and practical security engineering.

## References

1. **NIST FIPS 180-4: Secure Hash Standard (SHS)**  
   National Institute of Standards and Technology  
   [https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)  
   *Primary specification document for SHA-256 algorithm implementation*

2. **SHA-256 Algorithm Explained**  
   Qvault  
   [https://blog.boot.dev/cryptography/how-sha-2-works-step-by-step-sha-256/](https://blog.boot.dev/cryptography/how-sha-2-works-step-by-step-sha-256/)  
   *Step-by-step guide to understanding SHA-256 internals*

3. **Password Hashing: PBKDF2, Scrypt, Bcrypt and ARGON2**  
   OWASP (Open Web Application Security Project)  
   [https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)  
   *Industry best practices for secure password storage*

4. **Understanding Cryptographic Hash Functions**  
   Practical Cryptography for Developers  
   [https://cryptobook.nakov.com/cryptographic-hash-functions](https://cryptobook.nakov.com/cryptographic-hash-functions)  
   *Comprehensive overview of hash function properties and applications*

5. **Claude AI (Anthropic)**  
   [https://claude.ai](https://claude.ai)  
   *AI assistant used for implementation guidance and debugging support*