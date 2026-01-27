# Security Concepts

## 1. Passwords vs SSH Keys

### Explanation:

*Passwords* : Passwords are simple text secrets that a user types to authenticate.They rely on "something you know"
but they’re vulnerable to brute-force guessing, reuse across sites, and theft if stored or transmitted insecurely.

*SSH Keys* : SSH Keys are cryptographic key pairs (a public key and a private key) used for secure authentication.The server stores the public key, and the private key is on your machine.While connecting, SSH proves you have the private key without sending it over the network.It prevents brute-force guessing and don’t send your secret over the network, making them a stronger authentication method.

### Key Differences:

**Security Level:**

*Passwords* : Passwords generally provide a lower level of security because they are vulnerable to brute-force attacks, phishing, and dictionary attacks. 

*SSH Keys*: SSH keys offer a much higher level of security, as they use long cryptographic key pairs (typically 2048-bit or more), making them practically impossible to brute-force.

**Management:**

*Passwords* : Passwords must be remembered by users or stored in password managers, which increases the risk of reuse or exposure. 

*SSH Keys* : SSH keys are managed as files, where the private key remains on the user’s system and is often protected with an additional passphrase for extra security.

**Automation:**

*Passwords* : Password-based authentication is difficult to automate securely because it usually requires manual input or insecure hardcoding of credentials.

*SSH Keys* :  SSH keys are ideal for automation and scripting since they allow secure, passwordless logins without human intervention.

**Storage:**

*Passwords* : Passwords are stored on servers in hashed form, meaning the server must still manage and verify them during authentication.

*SSH Keys* :  With SSH keys, only the public key is stored on the server, while the private key remains securely on the client machine and is never shared.

## 2. Data Transformation vs Data Protection

### Explanation:

*Data Transformation* : Data Transformation is the process of changing the format  or structure of data to make it compatible with a specific system or to reduce its size.Examples include encoding, sorting, filtering, or translating characters -(data is altered for processing or readability).

*Data Protection* : Data protection safeguards data from unauthorized access or leaks using encryption, access control, and secure authentication. The focus is on keeping data safe, not changing its content.

### Key Differences:

**Purpose:**

*Data Transformation* : Data transformation is used to change the format of data for connectivity, storage efficiency, or easier display.

*Data Protection* :  Data protection is used to ensure confidentiality and integrity, preventing unauthorized access or tampering.

**Reversibility:**

*Data Transformation* : Data transformation is always reversible by anyone with the algorithm, since no secret is involved.

*Data Protection* : Data protection behaves differently: encryption requires a secret key to reverse the data, while hashing is intentionally irreversible.

**Examples:**

*Data Transformation* :  Encoding methods such as Base64 and URL encoding, as well as compression techniques like ZIP and Gzip.

*Data Protection* :  Encryption algorithms like AES and RSA, hashing algorithms such as SHA-256, and digital signatures.

## 3. PATH Injection / PATH Hijacking

### Explanation:

The `PATH` environment variable is a list of directories that the operating system searches through to find an program when you type a command.

PATH Hijacking occurs when an attacker manipulates the PATH variable (or a directory within it) to trick the system into running a malicious file instead of the intended legitimate program.This can lead to privilege escalation or execution of malicious code.

### How It Works:

When a script or program runs a command without specifying its full path (for example, using cat instead of /usr/bin/cat), the system searches for that command in the directories listed in the `PATH` environment variable.

If an attacker has write access to a directory that appears earlier in the `PATH` than the directory containing the real command, they can place a malicious executable with the same name in that directory.

When the command is executed, the system finds and runs the attacker’s version first instead of the legitimate one.

### Best Practices to Prevent PATH Hijacking

* Always use absolute paths (for example, /usr/bin/ls) in scripts, especially those running with high privileges.
* Avoid adding writable directories (such as . or /tmp) to the `PATH` variable.
* Regularly audit directory permissions for all directories included in `PATH`.
