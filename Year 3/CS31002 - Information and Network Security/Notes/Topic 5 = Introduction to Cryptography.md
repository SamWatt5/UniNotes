# Encryption Schemes
We intend to send a message to a recipient without it being compromised/accessed/changed in transit

## Communication over an insecure channel
Alice sends a message to bob over the internet. Anyone who wants to listen in will be able to read the message.
![[Pasted image 20251118111623.png]]
## Encryption Schemes (aka Ciphers) = encryption & decryption procedures
Alice sends a message to Bob over the internet. Nobody listening in will be able to understand the message, only Bob.
![[Pasted image 20251118111732.png]]
## Main Problem
Eve should not be able to learn the plaintext.
### What does this mean?
Alice uses key **k** on plaintext **m**, then ciphertext **c** is sent over the insecure channel. Bob can decrypt **c** with **k** to find **m**. Eve doesn't know **k**, so should not learn **m**.
![[Pasted image 20251118112209.png]]
# The history of Cryptography
The art of encrypting messages, mostly for military applications. Lack of precise definitions; ad-hoc design choices