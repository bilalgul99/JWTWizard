# JWT Token Editor

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue?logo=github)](https://yourusername.github.io/jwt-token-editor/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A web-based tool for inspecting, validating, and creating JSON Web Tokens (JWT) with support for multiple cryptographic algorithms.

## Features

- 🔍 Decode JWT tokens (header, payload, signature)
- 🔐 Verify tokens with secret/key
- ✏️ Create custom tokens with editable payload
- ⚙️ Support for multiple algorithms (HS256, HS384, HS512, RS256)
- ➕ Add/remove custom claims
- 📋 Copy generated tokens to clipboard

## Live Demo

The application is hosted on GitHub Pages:  
[https://yourusername.github.io/jwt-token-editor/](https://yourusername.github.io/jwt-token-editor/)

## Table of Contents

1. [JWT Fundamentals](#jwt-fundamentals)
   - [Structure](#structure-of-a-jwt)
   - [Algorithms](#supported-algorithms)
2. [Usage Guide](#usage-guide)
   - [Decoding Tokens](#1-decoding-a-token)
   - [Verifying Tokens](#2-verifying-a-token)
   - [Creating Tokens](#3-creating-a-custom-token)
3. [Development](#development)
4. [Security](#security-considerations)
5. [License](#license)

## JWT Fundamentals

### Structure of a JWT

A JWT consists of three Base64Url-encoded parts separated by dots (`.`):

header.payload.signature

1. **Header** - Contains metadata about the token:
   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```
   - `alg`: The hashing algorithm (e.g., HS256, RS256)
   - `typ`: Type of token (always JWT)

2. **Payload** - Contains the claims (statements about an entity):
   ```json
   {
     "sub": "1234567890",
     "name": "John Doe",
     "iat": 1516239022,
     "exp": 1516242622
   }
   ```
   Common claims:
   - `iss` (issuer)
   - `exp` (expiration time)
   - `sub` (subject)
   - `aud` (audience)
   - `iat` (issued at time)

3. **Signature** - Created by combining:
   - Base64Url encoded header
   - Base64Url encoded payload
   - A secret (for HMAC) or private key (for RSA)
   Using the specified algorithm

### Supported Algorithms

| Algorithm | Description                           | Key Type       | Security Level |
|-----------|---------------------------------------|---------------|----------------|
| HS256     | HMAC with SHA-256                     | Symmetric key | 128-bit        |
| HS384     | HMAC with SHA-384                     | Symmetric key | 192-bit        |
| HS512     | HMAC with SHA-512                     | Symmetric key | 256-bit        |
| RS256     | RSASSA-PKCS1-v1_5 with SHA-256        | Asymmetric keys | 2048-bit+     |

## Usage Guide

### 1. Decoding a Token

1. Paste your JWT token in the "Decode Token" section
2. Click "Decode"
3. View the decoded:
   - Header (including algorithm)
   - Payload (all claims)
   - Signature (raw)

### 2. Verifying a Token

1. Ensure the token is decoded first
2. Select the verification algorithm (must match token header)
3. Enter the appropriate key:
   - For HMAC: Enter the shared secret
   - For RSA: Paste the public key in PEM format
4. Click "Verify"
5. View verification result:
   - Green success message for valid tokens
   - Red error message for invalid tokens

### 3. Creating a Custom Token

1. Modify the payload fields:
   - Existing fields can be edited directly
   - Click "Add Field" to add new claims
   - Click "Delete" to remove claims
2. Select algorithm:
   - HMAC for simple shared secret
   - RSA for public/private key cryptography
3. Enter your key material:
   - For HMAC: Strong secret (min 32 chars)
   - For RSA: Private key in PEM format
4. Click "Generate Token"
5. Copy the generated token using the button

## Development

### Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/jwt-token-editor.git
   cd jwt-token-editor
   ```
2. Open `index.html` in a web browser

### Dependencies

- [CryptoJS](https://github.com/brix/crypto-js) - Cryptographic functions
- [js-base64](https://github.com/dankogai/js-base64) - Base64 encoding/decoding
- [jsrsasign](https://github.com/kjur/jsrsasign) - RSA support

### Project Structure

```
jwt-token-editor/
├── index.html          # Main application file
├── README.md           # This documentation
└── LICENSE             # MIT License file
```

## Security Considerations

1. **Key Management**:
   - Never commit actual secrets or private keys to version control
   - For RSA, use proper key generation (2048-bit minimum)
   ```bash
   openssl genrsa -out private.pem 2048
   openssl rsa -in private.pem -pubout -out public.pem
   ```

2. **Token Security**:
   - Always set reasonable expiration times (`exp` claim)
   - Validate all claims in production environments
   - Prefer RS256 over HS256 for distributed systems

3. **Browser Security**:
   - This tool runs entirely client-side
   - No tokens are sent to any server
   - Generated tokens only exist in your browser memory

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Key improvements in this version:

1. **Fixed Markdown Formatting**:
   - Proper headers and section organization
   - Correct code block formatting
   - Consistent list structures

2. **Enhanced Technical Details**:
   - Added security level information for algorithms
   - Included OpenSSL key generation commands
   - Expanded algorithm comparison table

3. **Improved Structure**:
   - Added table of contents
   - Better section organization
   - Clearer separation of concepts

4. **Added Practical Examples**:
   - Sample key generation commands
   - Clearer instructions for RSA key usage
   - More detailed verification process

5. **Complete Documentation**:
   - Covers all aspects from fundamentals to development
   - Includes security best practices
   - Provides clear usage instructions
