# SSH

## What is SSH?
- Secure Socket Shell
- Network protocol that provides secure access to remote locations
- `ssh user@0.0.0.0`

## How does it work?

### Encryption
- Can use symmetric or asymmetric encryption
- Symmetrical encryption allows both server and client to contribute to establishing a key, exchanged with key exchange algorithm
- One key is used to encrypt messages, and also decrypt messages
- Asymmetrical encryption uses private and public key
- Private key can be used to decrypt messages encrypted by the public key
- Public key can not decrypt any of its own messages, nor anything the private key sends

### Connection
- Server side listens on port 22
- Configuration can be changed in `/etc/ssh/sshd_config`
- Client initiates TCP handshake
- Checks if server is in `~/.ssh/known_hosts`
- Begins authentication, checks multiple authentications
- Offers publickey, attempts authentication
- If successful, begins session
- More detailed info using `ssh -v`

### Diffie-Hellman Exchange
- Exchange between two parties
- Agree on a large prime number as a seed value
- Agree on encryption generator
- Each party comes up with another prime number, secret from the other, used as a private key
- Private key, encryption generator and shared prime number are used to generate public key
- Public keys are then exchanged
- Each party uses the received public key, own private key and original shared seed to create a shared secret key, which will be the same secret key
- Shared secret 
