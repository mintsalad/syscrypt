# syscrypt (version 1.2.1)

### THIS PROJECT IS PUBLIC BUT NOT LIVE ** DO NOT DOWNLOAD ** ITS NOT READY

### ITS CURRENTLY PUBLIC BECAUSE WE HAVE TO TEST DOWNLOAD FUNCTIONALITY IN make.sh
### WE'll be ready for launch on <code>20.02/2026</code> once significant testing is complete
---

### Version 1.2.1
Hardened age wrapper for high-stakes security. Features identity-based auth, brute-force rate limiting, and a 15-minute "Nuclear Lockout." Built-in Pushover alerts for failed attempts. Hardened via garble obfuscation, string literal encryption, and SUID protection. A self-bootstrapping suite designed for anti-reverse engineering.

### Technical Architecture

syscrypt operates on a "Defense-in-Depth" model, moving beyond simple encryption to provide a managed security appliance.

* <b>Identity-Based-Auth:</b> Verifies a Master Public Key against internal state before allowing decryption.
* <b>Brute-Force Mitigation:</b> Implements exponential backoff and a hard "Nuclear Lockout" after 3 failed strikes.
* <b>Real-Time Monitoring:</b> Instant Pushover notifications for unauthorized access attempts or lockouts.
* <b>Build-Time hardening:</b> Uses garble to scramble logic, encrypt string literals (API keys), and strip debug symbols.
---

### The Suite

* <code>syscrypt</code>: Primary engine with auth and rate-limiting logic.
* <code>syscrypt-keygen</code>: Obfuscated identity generator.
* <code>syscrypt-batchpass</code>: Automated password handling.
* <code>syscrypt-inspect/decode/encode</code>: Hardened utility tools.

---

### Hardened Installation

syscrypt uses a Bootstrap Forge process. The make.sh script builds a temporary tool to generate unique keys, injects them into the source code, and then performs a final obfuscated compilation.

1. Clone the Repo:

```bash
git clone https://github.com/mintsalad/syscrypt.git
cd syscrypt
```


2. Run the Forge: The script will prompt you for Pushover API keys and whether to regenerate Master Keys.

```
  chmod +x make.sh
  ./make.sh
```
Running ./make.sh will also download the default Keys. Those need to be in place while building the binary.

---

### Security Warning
The SUID bit is required for <code>syscrypt</code> to manage lockout state files in protected directories.
Ensure <code>/root/.syscrypt</code> is only writable by <code>root</code>.

## Functionality

### Encrypt 

```bash
syscrypt [options]
```

| Flag | Description |
| :--- | :--- |
| -e | Explicitly tells <code>syscrypt</code> to encrypt. |
| -o FILE | Write the result to <code>FILE</code> instead of standard output. |
| -a | Encrypt to a PEM-encoded format. Useful for pasting keys into emails or chats. |
| -r | Encrypt to a specific public key. |
| -R FILE | Reads a list of recipients |
| -k | Pass your master password to encrypt |

### Decrypt

```bash
syscrypt [options]
```
| Flag | Description |
| :--- | :--- |
| -d | Explicitly tells <code>syscrypt</code> to decrypt the input|
| -i | Use a private key (identity file) located at <code>FILE</code>.|
| -k| Pass your master password to decrypt |

### Encode

```bash
syscrypt-encode -k [master password] -s [string]
```

| Flag | Description |
| :--- | :--- |
| -k | Your Master Password |
| -s | The string you want to encode |

### Decode

```bash
syscrypt-decode -k [master password] -s [string]
```

| Flag | Description |
| :--- | :--- |
| -k | Your Master Password |
| -s | The string you want to encode |




