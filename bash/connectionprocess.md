# Making the Connection

## SSH
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

## What happens when you curl or type in a website?
- Reads the url, and queries DNS for the IP address
- First checks cached domains previously visited on the OS or browser
- If no OS or browser cache match, queries DNS resolver
- DNS resolver usually provided by ISP, comes with DHCP assignment
- Can use open source alternates like Google or OpenDNS
- Resolver checks cache, then queries the root DNS servers
- There are 13 root DNS servers
- Root DNS servers do not provide the IP address, they direct to the top level domains (TLDs)
- TLDs hold the location of the authoritative name servers for each domain in the TLD such as **.com**
- The **.com** generic TLD will have the location of google.com's NS records, e.g. `ns1.google.com`
- DNS Resolver then queries one of the returned name servers for the IP of google.com
- The name server will know the IP and return a DNS record with the corresponding IP
- IP is returned to the user side and the connection can be made

### Notes
- Glue records glue the IP address of a domain to so that a the resolver can point the user to the name server to find the IP of the actual url
- More info at [here](http://blog.catchpoint.com/2014/07/01/dns-lookup-domain-name-ip-address/)

## IP Addressing and Subnetting

- IP Addresses are expressed by a 32 bit number, broken up into four 8 bit portions, e.g. `192.168.0.1`
- Subnet mask looks like `255.255.255.0`
- Separates out the network address and host address
- `192.168.123.0` is the network address, `000.000.000.132` is the host address
- A subnet mask of `255.255.255.192` divides into four networks of 62 hosts each
- First and last of all 0's or all 1's are invalid
- The four networks become:
  - `192.168.123.1-62`
  - `192.168.123.65-126`
  - `192.168.123.129-190`
  - `192.168.123.193-254`
