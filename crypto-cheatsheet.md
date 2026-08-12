## Generating Keys

### SSH — `ssh-keygen`

Generate an Ed25519 SSH key pair:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Generate an RSA key pair:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Common options:

| Option             | Meaning                 |
| ------------------ | ----------------------- |
| `-t ed25519`       | Key type                |
| `-t rsa`           | RSA key                 |
| `-b 4096`          | RSA key size            |
| `-C "comment"`     | Add a comment           |
| `-f ~/.ssh/my_key` | Specify output filename |
| `-N "password"`    | Set passphrase          |

Default files:

```text
~/.ssh/id_ed25519       # Private key — keep secret
~/.ssh/id_ed25519.pub   # Public key — safe to share
```

Show the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

---

### OpenSSL

#### Generate an RSA private key

```bash
openssl genrsa -out private.key 4096
```

Extract the public key:

```bash
openssl rsa -in private.key -pubout -out public.key
```

#### Generate a random symmetric key

Generate 32 random bytes (256 bits):

```bash
openssl rand -hex 32
```

Generate a random Base64 key:

```bash
openssl rand -base64 32
```

Useful for:

* AES encryption keys
* API secrets
* Tokens
* Other cryptographic secrets

> **Private keys and symmetric keys must be kept secret.** Public keys can be distributed to others.

---

### GPG — GNU Privacy Guard

#### Generate a GPG key pair

```bash
gpg --full-generate-key
```

Follow the prompts to select:

1. Key type
2. Key size
3. Expiration date
4. Name
5. Email
6. Passphrase

List your keys:

```bash
gpg --list-keys
```

List private keys:

```bash
gpg --list-secret-keys
```

#### Export a public key

```bash
gpg --armor --export KEY_ID > public-key.asc
```

Export a private key:

```bash
gpg --armor --export-secret-keys KEY_ID > private-key.asc
```

> **Never share your exported private key.** The `.asc` format is ASCII-armored and convenient for copying or sending keys.

#### Import a key

```bash
gpg --import public-key.asc
```

#### Get your key ID

```bash
gpg --list-keys --keyid-format LONG
```

---

### Quick Comparison

| Tool         | Typical key types   | Main use                                            |
| ------------ | ------------------- | --------------------------------------------------- |
| `ssh-keygen` | Ed25519, RSA, ECDSA | SSH authentication                                  |
| `openssl`    | RSA, EC, etc.       | TLS, encryption, certificates, general cryptography |
| `gpg`        | RSA, Ed25519, ECC   | Encryption, signing, identity                       |

### Public vs. Private

```text
              Key Pair
                 │
        ┌────────┴────────┐
        │                 │
   Public Key         Private Key
        │                 │
   Safe to share       KEEP SECRET
        │                 │
   Used to encrypt     Used to decrypt
   / verify            / sign
```

**Rule of thumb:**

* 🔓 **Public key** → share it
* 🔐 **Private key** → never share it
* 🔑 **Passphrase** → protect your private key
