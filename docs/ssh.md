# Introduction to SSH

SSH stands for Secure SHell and is a cryptographic network protocol. It enables accessing remote servers or embedded devices without passowrd validation. User name and passord infromation can be stolen while logging into a remote system since symmetrical encryption cannot be done on the remote system. However SSH uses asymmetric encryption to make the loggin process more secure.

## Symmetrical Encryption Algorithm
One function for encryption and decryption and is shared across the client and server. This function must be known by both systems in advance in order to support the encryption process. Problem arises when we are trying to access a remote system. How can we send it the encryption function in a way that is not vunerable to interception?

## Asymmetrical Encryption Algorithm
Unique pair of keys called the public key and private key to encrypt and decrypt network packets. The private key is secure to the home device whereas the public key is shared with anyone who wants to communicate with the home device.

Any remote system can communicate with the home device by using its public key to encrypt its network packets as it is sent through the network. The home device will use its private key to decrypt the packet contents on arrival. This works because the private key is secure to the home device and is very hard to guess using computer hashing.

In essence, asymmetric encryption shares the function for encryption publicly but secures the function for decryption to its local device.

## SSH Network Protocol Sequence
1. Client identifies themselves to the server by sharing its list of public keys
2. Server checks that the clients public key is registered in its database.
3. If present the server encrypts a secret message using the clients public key and sends it to the client.
4. Client then uses its private key to decrypt the contents and sends it back to the server for validation
5. If the pre-encrypted message matches the post decrpytion message the server verifies the client and SSH opens a tunnel between the client and the server from which all hashed / encrypted data is sent

## SSH Caveats
SSH is a service, so its not available until the target system has configured and employed an ssh listener service.