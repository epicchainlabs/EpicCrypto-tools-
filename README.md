# EpicCryptoTools++

## Overview

EpicCryptoTools++ is a powerful cryptography library implemented in C++ designed to cater to the needs of the modern blockchain ecosystem. It is a comprehensive tool aimed at developers looking to integrate advanced cryptographic functionalities into their applications. This library is particularly useful for those working within blockchain environments, offering robust and efficient cryptographic operations.

## Project Context

EpicCryptoTools++ is part of the EpicChain project, which focuses on building a cutting-edge blockchain ecosystem. The library is designed to complement EpicChain’s suite of tools and services, providing essential cryptographic functions required for secure blockchain transactions and operations.

## Getting Started

### Building EpicCryptoTools++

To get started with EpicCryptoTools++, follow these steps to build the library and the accompanying command-line tool, `cryptool`:

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/epic-chain/epiccryptotools++.git
   cd epiccryptotools++
   ```

2. **Initialize Submodules:**
   Ensure that all required submodules are initialized:
   ```bash
   git submodule update --init --recursive
   ```

3. **Build Dependencies:**
   - **OpenSSL Engine:**
     ```bash
     make vendor
     ```

4. **Build the Library and Tool:**
   Compile the EpicCryptoTools++ library and the `cryptool` executable:
   ```bash
   make
   ```

   After the build process, the `cryptool` executable will be located in the `bin/` directory.

### Using the Command-Line Tool

The `cryptool` command-line interface (CLI) provides an easy way to interact with the cryptographic functionalities of EpicCryptoTools++. 

**Launching `cryptool`:**
   ```bash
   ./bin/cryptool
   ```

**Interactive CLI:**

Upon launching, you will be greeted with a simple terminal interface:

```
===============================================
Welcome to cryptool: a library for devs
===============================================
Type 'exit' to finish program (or 'help')
```

**Available Commands:**

- `help` - List all available commands and their options.
- `set [ecc hash] [secp256r1 | sha256]` - Set the elliptic curve or hash type.
- `gen [ECC_TYPE] [keypair pubkey privkey] [compressed uncompressed] [PRIVATE_KEY]` - Generate keys.
- `hash [hash160 hash256 sha256 ripemd160 none] [TEXT_OR_BYTES]` - Compute hash of input data.
- `bytes [reverse length] [TEXT_OR_BYTES]` - Reverse bytes or calculate byte length.
- `sign [ECC_TYPE] [PRIVATE_KEY] [HASH_TYPE] [TEXT_OR_BYTES]` - Sign data using a private key.
- `verify [ECC_TYPE] [PUBLIC_KEY] [SIGNATURE] [HASH_TYPE] [TEXT_OR_BYTES]` - Verify a signature.
- `rand [BYTE_COUNT]` - Generate random bytes.
- `show [engine]` - Display the underlying cryptographic engine.

**Examples:**

1. **Hashing an empty string with SHA256:**
   ```bash
   > hash sha256 ""
   hash: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
   ```

2. **Generating a random keypair for elliptic curve `secp256r1`:**
   ```bash
   > set ecc secp256r1
   CURVE SET TO 'secp256r1'

   > gen ecc keypair
   public key (compressed format): 037c50d797720fefe9194ecd5b4ef3c25b3791abb45639aa8453d110bae08a945a
   private key: 13043155bf3e00b6e6352ffafba9f7fa96704de08c7db2fe810a92d644199258
   ```

3. **Signing and verifying a payload:**
   ```bash
   > rand 50
   generated bytes (50): 9ec1171a37169a9e4b38726127730d64bed872f7840afeaf54028834e531e2d89a8d269f78eb426628f6cc3dc3ad99a2a43b

   > gen ecc keypair
   public key (compressed format): 02bff10e1aa6b544fd9fc07b28488425931e6a0d9c44b5f3fd6b7c2f489a9987ad
   private key: 4f7f56c979e2fafbe26c5d9164066ea581b4e08a52805ca377d573a853f0aa5e

   > sign ecc 4f7f56c979e2fafbe26c5d9164066ea581b4e08a52805ca377d573a853f0aa5e hash 9ec1171a37169a9e4b38726127730d64bed872f7840afeaf54028834e531e2d89a8d269f78eb426628f6cc3dc3ad99a2a43b
   signature: 7b6d7a7b0738f98bfcb7f94bcc7f5e4c4dd3469d321235d52117711096360e8eb133d42831f01a603d94574b626eb68b2d3686d7e75433b8d69874bc4f3948ce

   > verify ecc 02bff10e1aa6b544fd9fc07b28488425931e6a0d9c44b5f3fd6b7c2f489a9987ad 7b6d7a7b0738f98bfcb7f94bcc7f5e4c4dd3469d321235d52117711096360e8eb133d42831f01a603d94574b626eb68b2d3686d7e75433b8d69874bc4f3948ce hash 9ec1171a37169a9e4b38726127730d64bed872f7840afeaf54028834e531e2d89a8d269f78eb426628f6cc3dc3ad99a2a43b
   verification result: 1
   ```

### Command-Line Mode

For embedding `cryptool` in scripts or automated processes, use the command mode `-c` to execute commands directly:

```bash
./bin/cryptool -c "rand 5 ; rand 10 ; rand 1"
d070440077
a313e92ddb08a706b23a
9b
```

You can also execute commands from a file:

```bash
cat scripttest.txt
rand 5
hash sha256 0x0001
rand 10

./bin/cryptool -f scripttest.txt
b2c6db7ab4
b413f47d13ee2fe6c845b2ee141af81de858df4ec549a58b7970bb96645bc8d2
635c59ca7d16aab29eb6
```

## Why C++?

C++ is chosen for its efficiency and interoperability with a wide range of languages and platforms. Unlike high-level languages that may not be suitable for lightweight or resource-constrained environments, C++ allows for direct control over system resources and optimizations, making it ideal for cryptographic operations that require performance and precision.

## Build Instructions

EpicCryptoTools++ supports multiple implementations, each with its own set of dependencies:

### C++ Native Implementation

This version relies on the [csBigInteger](https://github.com/neoresearch/csbiginteger.cpp) library for big integer operations. On Debian-based systems, install the required dependencies:

```bash
make vendor
```

### OpenSSL Implementation

For the OpenSSL implementation, ensure you have `libopenssl` installed. Use the following command to install dependencies:

```bash
make vendor
```

### Testing

To run tests, ensure you have cloned the project with submodules. Execute the following command to build and run tests:

```bash
make test
```

## C++ Standards and Recommendations

### C++ Version

The project currently adheres to C++11 standards to maintain compatibility across various tools and modules. Future updates will aim to migrate to C++17, provided it does not disrupt compatibility.

### Code Style

- **IDE Recommendations:**
  - **Visual Studio Code:** Install extensions for C++ development, such as C/C++ (0.23.0-insiders2), C++ Intellisense (0.2.2), and GoogleTest Adapter (1.8.3).
  
- **Formatting:**
  - **Style:** Mozilla style with an indentation level of 3 spaces.
  - **VS Code Configuration:**
    ```json
    {
        "[cpp]": {
            "editor.tabSize": 3,
            "editor.detectIndentation": false
        },
        "C_Cpp.clang_format_fallbackStyle": "{ BasedOnStyle : Mozilla , ColumnLimit : 0, IndentWidth: 3, AccessModifierOffset: -3}"
    }
    ```

-

 **Documentation:** 
  - Maintain up-to-date documentation using Doxygen for inline comments and module descriptions.
