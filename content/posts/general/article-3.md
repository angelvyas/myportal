---
title: "SSH - Secure Shell"
date: 2025-05-06
draft:  false   
featured: false  
description: "SSH"
thumbnail: "/posts/general/images/ssh.png"
featureImage: "/posts/general/images/ssh.png" 
shareImage: "/posts/general/images/ssh.png"
author: "Angel Vyas"
tags:
    - Info
categories:     
    - General
---

SSH (Secure Shell) is a `cryptographic network`(encryption and decryption) protocol that allows secure communication between a client and a server over an unsecured network. It encrypts all data sent between your computer and the remote machine, keeping passwords, commands, and files safe from hackers.

### Why SSH?
SSH is required because older protocols like Telnet, FTP, and rlogin transmit data — including usernames and passwords — in plain text, making them vulnerable to eavesdropping and attacks.

🔒 **Why SSH is better:**
- `Encryption`: Unlike Telnet or FTP, SSH encrypts all communication.
- `Authentication`: SSH uses secure methods like public-key authentication.
- `Integrity`: It ensures that data isn't altered during transmission.
- `All-in-One`: SSH can replace multiple insecure tools (e.g., Telnet, FTP, rsh) with a single secure solution.

`SSH uses three main types of encryption to secure communication:`
- Symetric Encryption.
- Asymmetric Encryption.
- Hashing.

### Symmetric Encryption.
- Both client and server use the same secret key to encrypt and decrypt data.
- Key is securely exchanged during the handshake.
- It's fast and used for the actual data transfer.
- Example: AES, ChaCha20 (Algorithms used.)

![](../images/se.png)

> Symmetrical encryption is often called shared key or shared secret encryption.

### Asymmetric Encryption.
- Uses a key pair: a public key and a private key.
- Helps in secure login and key exchange.
- server has the public key, and client has the private key.
- Example: RSA, Ed25519.(Algorithms used.)

![](../images/ae.png)

### Hashing (MAC – Message Authentication Code).
- Ensures data integrity — checks if the data was changed in transit.
- Example: HMAC-SHA256(Algorithms used.)

</br>

### Generating SSH Key:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
`If you are using a legacy system that doesn't support the Ed25519 algorithm, use:`
``` bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

**For example let's create a ssh key for my system:**
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
then you'll get these:

```bash 
Enter file in which to save the key (/home/you/.ssh/id_algorithm):[enter]
Enter passphrase (empty for no passphrase): [Type a passphrase] or [enter].
Enter same passphrase again: [Type passphrase again]or [enter].
```

then you'll get your public/private key.

> just type : ls -al, go to .ssh folder, then cat id_rsa to get private key, and cat id_rsa.pub to get public key.
Then you can share this public key with the server, you want to connect with.



