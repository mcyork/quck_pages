# Private Key Decryptor

A secure, client-side tool for decrypting encrypted private keys without exposing them to the file system or network.

## Overview

This tool solves a common problem in certificate management: users receive encrypted private keys and need to decrypt them for use in applications, but don't want to use command-line tools or save unencrypted keys to disk.

**The solution:** A browser-based decryptor that handles everything locally and securely.

## Why This Tool is Safe

### 🔒 **Everything Runs Locally**
- All cryptographic operations happen in your browser
- No data is sent to any server or external service
- Works completely offline after the initial page load

### 🚫 **No File System Exposure**
- Decrypted keys are only displayed in memory
- No temporary files created on your computer
- No risk of leaving unencrypted keys on disk

### 🛡️ **Security Features**
- Passwords are automatically cleared after decryption
- Uses industry-standard crypto libraries (node-forge)
- Same cryptographic algorithms as OpenSSL
- No browser storage or caching of sensitive data

### 📋 **Clean Workflow**
1. Paste encrypted key → Enter password → Decrypt → Copy result
2. All sensitive data stays in browser memory only
3. Close browser tab to completely clear everything

## Supported Key Formats

The tool supports the same encrypted private key formats that OpenSSL generates:

- **PKCS#8 Format** (`-----BEGIN ENCRYPTED PRIVATE KEY-----`)
- **Traditional RSA Format** (`-----BEGIN RSA PRIVATE KEY-----` with `Proc-Type: 4,ENCRYPTED`)
- **DSA and EC Keys** (encrypted variants)

### Supported Encryption Algorithms
- AES (128, 192, 256-bit)
- 3DES
- DES
- RC2, RC4
- All standard algorithms used by OpenSSL

## How to Use

### Method 1: Paste Key Text
1. Copy your encrypted private key (including the `-----BEGIN` and `-----END` lines)
2. Paste into the large text area
3. Enter your password
4. Click "Decrypt"
5. Copy the decrypted key from the result area

### Method 2: Upload Key File
1. Click "Upload Encrypted Private Key File"
2. Select your `.pem`, `.key`, or `.txt` file
3. Enter your password
4. Click "Decrypt"
5. Copy the decrypted key from the result area

## Technical Details

### Libraries Used
- **node-forge** (v1.3.1): Handles PEM parsing and cryptographic operations
- Loaded from cdnjs.cloudflare.com CDN

### Browser Requirements
- Modern browser with JavaScript enabled
- Chrome, Firefox, Safari, Edge (recent versions)
- No additional plugins or extensions required

### What Happens During Decryption
1. Tool parses the PEM format to extract encrypted data
2. Identifies the encryption algorithm from the key headers
3. Uses your password to decrypt the key material
4. Reconstructs the private key in standard PEM format
5. Displays the result for copying

## Comparison to OpenSSL

Instead of running commands like:
```bash
# Save encrypted key to file
cat > encrypted_key.pem

# Decrypt key (creates unencrypted file)
openssl rsa -in encrypted_key.pem -out decrypted_key.pem

# Use decrypted key, then cleanup
rm decrypted_key.pem
```

You can now:
1. Paste → Enter password → Copy result
2. No files created or left behind

## Security Best Practices

### ✅ **Safe Practices**
- Use this tool on a trusted computer
- Close the browser tab when finished
- Don't leave the page open with decrypted keys visible
- Use strong, unique passwords for your private keys

### ⚠️ **General Security Reminders**
- Never share your private keys or passwords
- Only decrypt keys when you need to use them
- Keep your encrypted key files secure
- Use this tool in a private browsing session for extra privacy

## Installation

**Option 1: Download and Use Locally**
1. Save the HTML file to your computer
2. Double-click to open in your browser
3. No internet required after first load

**Option 2: Host on Internal Server**
1. Place the HTML file on your web server
2. Access via your internal URL
3. Still runs entirely client-side

## Troubleshooting

### "Failed to decrypt" Error
- **Most common cause:** Incorrect password
- **Other causes:** Corrupted key file, unsupported encryption format
- **Solution:** Verify password, ensure complete key text is pasted

### "Invalid PEM format" Error
- **Cause:** Missing or malformed PEM headers/footers
- **Solution:** Ensure key includes `-----BEGIN` and `-----END` lines

### Key Not Recognized
- **Cause:** Unencrypted key or unsupported format
- **Note:** This tool only handles encrypted private keys

## Why Not Just Use OpenSSL?

OpenSSL is powerful but has drawbacks for many users:
- Requires command-line knowledge
- Creates unencrypted files on disk
- Complex syntax and parameters
- Not user-friendly for occasional use

This tool provides the same cryptographic security with a much better user experience.

## Development

The tool is self-contained in a single HTML file with:
- Vanilla JavaScript (no frameworks)
- CSS for clean, responsive design
- node-forge library for cryptographic operations
- No build process or dependencies

## License and Disclaimer

This tool is provided as-is for legitimate certificate management purposes. Users are responsible for the security of their private keys and passwords. Always follow your organization's security policies when handling cryptographic material.

---

**Questions or Issues?** 
This tool implements standard cryptographic practices and should handle any encrypted private key that OpenSSL can decrypt.
