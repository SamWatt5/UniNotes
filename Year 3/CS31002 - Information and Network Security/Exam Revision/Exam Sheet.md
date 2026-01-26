# Introduction to Information and Network Security
## Topic 1 - Introduction to Information and Network Security
### Key definitions:
**Cybersecurity** - prevention & detection of improper actions by users of information systems
**Network security, web security, database security,...** - same as above but for their specific domains
**Information Security** - more general, deals with proper use of information, independent of computer systems
**Confidentiality** - Information is not make available or disclosed to unauthorised entities
**Integrity** - Information is accurate and complete
**Availability**  - Information is accessible and usable upon demand by an authorised entity
### Core ideas:
Why is security useful:
- Can cause loss of data
- Possible huge costs
- Disrupt functions of systems
- Can Cause leaks of data
Why are systems insecure?
 - Limited resources
	 - Must balance cost with potential loss
 - Changing Environment
 - Complexity of software
### Examples:
Equifax Website Hack 
Sony PlayStation Hack
WannaCry Ransomware
### Common exam questions:
## Topic 2 - Security Risk Assessment
### Key definitions:
**Asset** - What are we protecting?
**Threat Agent** - Who is the attacker?
**Threat** - Cause of an unwanted event that may harm asset
**Vulnerabilities** - What can be exploited by a threat?
**Countermeasure** - What can be done to detect/deter/deny the attack?
**Risk** - (Impact to asset from exploit of vulnerability)
### Core ideas:
Risk is the chance of a threat and its impact
Risk Assessment:
1. Identify assets, threat agents, and threats
2. Identify vulnerabilities
3. Measure probability of occurrence and impact

Risk Mitigation
1. Prioritise the risks
2. Identify countermeasures
3. Evaluate the countermeasures:
	- How well do they reduce the risk
	- How expensive are they
	- what trade-offs and new risks do they bring
4. Implement countermeasures
### Examples:
£20,000 impact x 50%/year probability = £10,000/year risk
### Common exam questions:

# Network Programming and Security
## Topic 3 - Transmission of Data through Networks/Sockets
### Key definitions:
**Socket** - A way for the operating system to provide network capabilities to applications
### Core ideas:
Most operating systems provide network capabilities to user applications through interfaces called sockets
From a developer POV, sockets are an API to the transport layer functionalities.
### Examples:
### Common exam questions:
## Topic 4 - Securing Sockets and Data over Networks
### Key definitions:

### Core ideas:
Sockets from client POV:
1. Create a socket
2. Create a SSL/TSL context
3. Wrap the socket in the SSL/TLS context
4. Connect the wrapped socket to IP:port
5. Loop sending/receiving data with the server
6. Close the connection

Sockets from server POV:
1. Create a socket
2. Bind the socket to an IP:port
3. Listen for new connections
4. Create a SSL/TLS context
5. Load certificate and keys in the SSL/TLS context
6. Loop accepting new client connections
	1. Get the client socket
	2. Wrap the client socket in the SSL/TLS context
	3. Loop sending/receiving data with that client
	4. Close this client connection
7. Close the server socket
### Examples:
### Common exam questions:

# Introduction to Cryptography and Symmetric Ciphers
## Topic 5 - Introduction to Cryptography
### Key definitions:
**Plaintext** - The text being encrypted
**Ciphertext** - The text after encryption
**Brute-Force Attack** - Check all possible keys on ciphertext to get plaintext
**Encryption Scheme** - pair of algorithms Enc & Dec:
- **Enc**: $K \times M \rightarrow C$
- **Dec**: $K \times C \rightarrow M$
**Kerckhoffs' Principle** - A cipher must remain secure even if the adversary knows everything about the cipher
**Security by Obscurity** - Not respecting Kerckhoffs' Principle
**Perfect Secrecy** - An encryption scheme is perfectly secret, if the adversary learns no additional information about the plaintext after observing the ciphertext
**Shannon Theorem** - For a perfect encryption scheme (Enc, Dec), then $|K| \geq |M|$
**One-Time Pad** - A perfectly secret encryption scheme. XOR the ascii values' bits with a one-time key. i.e. $1001000 \oplus 1101011 = 0100011$ that is impractical due to Shannon's Theorem
**Computational secrecy** - $m$ and $Enc_m(m)$ are independent "from the point of view of a computationally limited adversary"
**Efficiently computable** - A task is this if it is polynomial-time computable on a probabilistic Turing Machine
**IND-CPA Security** - (Enc, Dec) has indistinguishable encryptions under a chosen-plaintext attack (IND-CPA) if every randomized polynomial time adversary guesses b correctly in the CPA game with probability at most $0.5+\varepsilon(n)$ where $\varepsilon$ is negligible
**CPA-Secure** - If a computationally bounded adversary cannot do better than random guessing
**ciphertext-only attack** - the adversary has no information about the plaintext
**known plaintext attack** - the adversary learns the plaintext, but they are drawn from some distribution that the adversary does not control
**chosen-plaintext attack** - the adversary chooses the plaintexts.
**chosen ciphertext attack** - the adversary may additionally query a decryption oracle
### Core ideas:
Send a message to recipient without it being accessed/changed in transit
Motivation for Kerckhoffs' Principle
- Unrealistic to assume design main secret (i.e. reverse engineering)
- Short keys are easier to *protect, generate* and *replace*
- Design details can be discussed and analysed in public
- harder to put backdoors into the cipher
### Examples:
### Common exam questions:
## Topic 6 - Stream and Block Ciphers
### Key definitions:
**Symmetric Encryption** - Form of encryption where the same key is used to encrypt and decrypt
**Stream Cipher** - A cipher than is used to encrypt a message stream continuously, one bit or byte at a time.
**RC4** - Stream Cipher System used for WEP, WPA and SSL/TLS. Efficient and simple but has some security flaws.
**Block Cipher** - A cipher that encrypt a message in blocks, instead of bit by bit.
**ECB** - (Electronic Code Book) An old, insecure form of block cipher, which uses the same key for every block. All the plaintext that's the same, gives the same ciphertext. - each block can be done in parallel
**CBC** - (Cipher Block Chain) Like ECB, but each block's plaintext is XOR'd with the previous block's ciphertext - cannot be parallelised well. If tampered with along the way, changes whole message
**IV** - (Initialisation Vector) XOR'd with the first message in a CBC. (Not Secret)
**CTR** - (Counter Mode) a counter is encrypted, then this is XOR'd with the plaintext block to get ciphertext. counter is increased each block.
### Core ideas:
Pseudorandom generators can shorten length of key. Essentially have key as seed for the generator, then use the number generated for encryption.
### Examples:
### Common exam questions:
## Topic 7 - Hash Functions and Message Authentication Codes (MACs)
### Key definitions:
**Hash Function** - A form of encryption that takes a plain text and turns it into a cipher text of a fixed size
**Message Authentication Code** - (MAC) is a pair of algorithms (tag, vrfy), where tag: $K\times M \rightarrow T$, vrfy: $K\times M\times T \rightarrow \{true, false\}$ and tag and vrfy satisfy the following correctness condition: for every $k$ in $K$, $m$ in $M$: vrfy($k,m,$tag($k,m$)) = true
- *tag* - a tagging algorithm
- *vrfy* - verification algorithm
- $K$ is the set of keys
- $M$ is the set of plaintexts
- $T$ is the set of tags
### Core ideas:
Hash functions are:
- Preimage resistant: Given a hash value it is difficult to find the input
- Collision resistant: It is difficult to find two inputs that hash to the same output
- second preimage resistant: it is difficult, given one input, to find a second input that hashes to the same output
second preimage resistance and collision resistance are similar, but collision resistance is finding *any* matching pair, and second preimage resistance is knowing one input, finding another input that maps to the same output.
If Alice sends message $m$ to Bob with tag$_k(m)$, and Eve intercepts this, Eve should not be able to compute a valid tag t' on any other message m'.
If vryfy$_k$(m,t) = true then we say that t is a valid tag for message m.
Constructing MACs from Hash Functions:
- MAC$_k$(m) = H(k||m) <- hash of concatenation of key and message, insecure
- Better idea: HMAC
	- HMAC$_k$(m) = H((k $\oplus$ opad)||H(k $\oplus$ ipad || m))
	- where ipad = 0x363636..., opad = 0x5C5C5C5C...
	- i.e. HMAC-SHA256$_k$(m) = SHA256$((k $\oplus$ opad)||H(k $\oplus$ ipad || m))
Establishing Secure Channels:
- 3 options:
	- Encrypt-and-MAC:
		- c := Enc$_{k1}$(m) and t := Tag$_{k2}$(m), send (c,t)
	- MAC-then-encrypt:
		-  t := Tag$_{k2}$(m) and c := Enc$_{k1}$(m || t), send c
	- Encrypt-then-MAC:
		- c := Enc$_{k1}$(m) and t := Tag$_{k2}$(c), send (c,t)
- or, design an authenticated encryption from scratch:
	- A popular method: Galois/Counter Mode (GCM)
### Examples:
### Common exam questions:

# Human Factors, Passwords and Phishing
## Topic 8 - Passwords
### Key definitions:
**Dictionary attack** - An attack that tries common or likely passwords first
**Rainbow Table** - A precomputed time-memory trade-off attack that uses hash chains to reverse unsalted password hashes
**Salt** - A random value generated per user and combined with the password before hashing
### Core ideas:
### Examples:
### Common exam questions:
## Topic 9 - Phishing
### Key definitions:
### Core ideas:
### Examples:
### Common exam questions:

# Web App Vulnerabilities and Attacks
## Topic 10 - Web Application Vulnerabilities and Attacks
### Key definitions:
**SQL Injection** - (SQLi) SQL command is inserted into an input field and run on the database
**Cross Site Scripting** - (XSS) Scripts are injected into websites and run on browsers
Types of XSS:
- Stored:
	- Stored Server XSS - Malicious user input is stored in target server (i.e. in database or message forum). Client receives stored data from server
	- Stored Client XSS - Malicious user input is stored in the client's browser (e.g. added to HTML5 localStorage). Data may not be sent to the server.
- Reflected:
	- Reflected Server XSS - Malicious user input is received by server and sent back to browser (e.g. error/confirmation message)
	- Reflected Client XSS - Malicious user input is displayed by client's browser (added to DOM), but data is not stored and may not be sent to server.
**Cross-Site Request Forgery** - (CSRF) Victim's browser is tricked into sending an authenticated request to a website without user consent.
**Active Data Uploads** - Where a user can upload a file e.g. an image, they see that your site uses php, java,..., then they upload a file i.e. evilphpfile.php, which is saved to the server, the user then goes to `mysite.com/uploads/evilphpfile.php` and runs the file.
**Denial of Service** - (DoS) Class of attacks on availability of a service
**Distributed Denial of Service** - (DDoS) DoS attack where many, distributed, willing or unwilling participants contact victim
### Core ideas:
XSS
- Attackers inject scripts through a form, link, etc.
- Web server trusts client request, and sends malicious script
- Client's browser execute malicious script that is receives
Defending against XSS
- User input must be securely handled in *both* server *and* client side code.
- Stored and reflected XSS are countered by the same defense mechanisms
- Server XSS:
	- First line of defence: Use context-sensitive (server side) output encoding
	- Input validation: stop browser interpreting it as code. Use whitelists instead of blacklists for tokens.
- Client XSS:
	- Best: Avoid client side document rewriting, generate dynamic pages server-side
	- use safe JavaScript APIs/methods
	- Input validation
	- Context-sensitive output encoding (in the browser) before calling unsafe JS methods.
CSRF
- Attacker provides script or link with malicious side-effects for victim
- Client's browser acts on script/accesses provided link thus asking server to perform unwanted action
- Server executes client's request and performs attackers requested change
XSS vs CSRF:
- XSS: Browser executed malicious injected code
- CSRF: Server receives malicious request from browser and acts on it
Defending against CSRF:
- Server cannot distinguish user or attacker requests
- Using POST instead of GET *does not* protect from CSRF
- Valid requests for critical state changes (e.g. money transfers) must include unpredictable tokens. This can be done with challenge-response mechanisms
- Protect yourself: Do security critical things in one browser without multitasking. Logout, quit browser, then go back to other business
Protecting against active data upload:
- Put any uploads outside of the path to the document root
	- This prevents the attacker from directly accessing the file
- Create a new, unpredictable file name
	- Original names can be stored in a lookup table
Denial of Service
- 2 options to attack availability:
	- Break service
	- Overload service/starve it of a resource
- Break the service:
	- Ping of death: Send malformed (e.g. larger-than-expected) packet to crash victim's service
	- Permanent DoS: Exploit security flaw to replace device's firmware with non-functional firmware
- Overload/Starve the service
	- Stops the service of legitimate requests
	- Techniques:
		- Consume too much bandwidth
		- Create too many requests
		- Create time-consuming requests
		- Make the service hard to reach by overloading a nearby router with bogus requests
DDoS
- Frequently carried out using botnets:
	- Find wide-spread vulnerability
	- Exploit it, install your code
	- Lets bots turn more vulnerable machines into bots
Defending against DoS
- Distributed replication: Replicate service with different, functionally similar technologies
	- use different hardware vendors for routers, servers, hard disks
	- run different operating systems
	- install different applications
- (Local) Monitoring & Filtering with Routers/Switches
	- Rate limiting
	- Simple request filtering (based on IP addresses, particular request strings)
	- filtering after deep packet inspection
- Upstream Filtering: Traffic is first passed through a cleaning centre (e.g. Cloudflare, Incapsula, ...) and then passed on to the server
- Puzzles and cookies
	- protects server by requiring that client spends time solving a hash puzzle whose solution is easy to verify for the server
IoT Security
- Cheap IoT devices are frequently full of security vulnerabilities
- Many of these devices will never receive security updates
- This poses a threat to all devices that are on the same network and in some cases to the Internet at large (i.e. DDoS)
### Examples:
### Common exam questions:
# Public Key Cryptography
## Topic 11 - Public Key Cryptography
### Key definitions:
**Symmetric Encryption**: One key is used for both encryption and decryption
**Asymmetric Encryption**: A public key is used to encrypt, and a different, private key is used to decrypt

### Core ideas:
How can Alice and Bob communicate securely?
- By exchanging a secret key
- How can Alice communicate a secret key to Bob?
	- Meet in person
	- Rely on trusted intermediaries
	- Use a secure channel (need to have previously exchanged keys)
- Solution: Pre-deploy pairwise keys:
	- Company gives every employee $P_i$ a separate key $k_{ij}$ to communicate with every $P_j$
	- This requires a quadratic number of keys:
		- High storage and deployment costs
		- Key distribution, key revocation, and key rotation for one user affects all users
- Solution: Key Distribution Centres:
	- Some server, a Key Distribution Center (KDC) "gives the keys" to users on the fly
	- Feasible if users are working in one company
	- infeasible on the internet
	- Relies on honesty of KDC
	- KDC needs to be permanently available
- Solution: **Public Key Cryptography**
One way functions:
- easy to compute, hard to invert
- We don't know whether these exists, but we have some candidates:
	- Pre-image resistant hash functions
	- Multiplication of two large prime numbers
	- Discrete Exponentiation (e.g. exponentiation modulo a large prime number)
Diffie-Hellman Key Exchange
- Alice's public key $g^a$ and Bob's public key $g^b$. 
- Alice knows $a$ and bob knows $b$, these are private keys. 
- Alice calculates $(g^b)^a$ and bob calculates $(g^a)^b)$.
- Using maths, $g^{ba} = g^{ab}$, so this is the key used for encryption
Public Key Cryptography
- Instead of using one key ***k***, use 2 keys (*pk*, **sk**), where *pk* is used for encryption and **sk** is used for decryption
- *pk* is the public key
- **sk** is the private key, and must be kept secret
ECC Encryption
- idk
RSA Cryptosystem
- A system where a public key (N,e) is used for encryption
- private key (N,d) is used for decryption
- Public key is the product of two very large prime numbers, N, as well as an integer, e, used to encrypt
- Private key is N, as well as an integer d, which is calculated using the two prime factors of N, as well as e
Problem with Textbook RSA
- Deterministic! if the same message is encrypted twice then the two ciphertexts are the same!
- If the set of probable plaintexts is small, the adversary can check all possible messages
- if there are only two likely plaintext messages, "yes" and "no", then the adversary can decrypt the ciphertext!
- To fix this we can add random padding to the message, so it is different every time
### Examples:
### Common exam questions:
# Digital Signatures and Public Key Infrastructures
## Topic 12 - Digital Signatures
### Key definitions:
**Digital Signatures** - a way of showing who sent a message
**Non-Repudiation** - proof of the integrity and origin of data
**Tag** - value produced by a digital signature, attached to message and used to verify authenticity and integrity (See Topic 7)
**iff** - if and only iff
### Core ideas:
Private keys are used to sign a message, Public keys are used to verify signatures.
Private key is used to compute a tag,
Public key is used to verify correctness of the tag
Digital signatures are:
- publicly verifiable
	- Anyone can check that a message coming from Alice actually comes from Alice
- transferable
	- If Bob sends a message from Alice to Wilma, and says "this is from Alice", then Wilma can check this
- provide non-repudiation
	- If Alice sends a message to Bob, and Bob says to a judge "i got this from Alice", but Alice says "I never sent this!", there is proof that Alice sent the message
MACs are not publicly-verifiable
Textbook RSA Signatures:
- sign$_{(d,N)}$(m) = m$^d$ mod N
- vrfy$_{(e,N)}$(m, $\sigma$) = true iff $\sigma^e$ = m mod N
- $\sigma$ is a valid signature on m
This can be forged!
- given public key (N,e):
- Eve selects random $\sigma$ and computes m=$\sigma^e$ mod N
- $\sigma$ is a valid signature on m
Solution: 
- Use a collision-resistant hash function H, then compute RSA function
- sign$_{d}$(m) = H(m)$^d$ (mod N)
- vrfy$_{e}$(m, $\sigma$) = true iff $\sigma^e$ = H(m) (mod N)
Hash and Sign ($\uparrow$)
- generic construction that takes
	- a signature scheme that works on "short messages", and
	- a collision resistant hash function
- and transforms it into
	- a signature scheme that works on "long messages"
- i.e. to sign message m, sign the hash of m
- to verify message m, verify $\sigma$ with H(m)
### Examples:
### Common exam questions:
## Topic 13 - Public Key Infrastructures
### Key definitions:
**Digital Certificate** - binds an identity and purpose to a public key
**Public Key Infrastructure** - (PKI) a set of policies and procedures to manage (create, distribute, store, revoke) digital certificates.
**Certificate Authorities** - (CAs) An entity which knows both public and private keys, and links them to an ID
**Certificates** - a data structure that binds an entity (and purpose) to a key
### Core ideas:
We know that public/private keys are generated in private - so how can Bob prove that "Alice's" public key belongs to Alice, and not to Eve.
A PKI can be based on
- Certificate Authorities
	- Alice can distribute her public key or digital signatures with her certificate she recieves from the CA
	- Anyone who trusts the CA can verify that "Alice's" pk is Alice's
- Web of Trust (PGP/GnuPG)
- Blockchain
Certificates
- Parameters: issuer, expiration date, purpose of the public key
- Validating an X.509 certificate:
	- Certificate recipient obtains public key of CA that signed the certificate
	- Recipient validates certificate by computing has of *non-signature fields* and checking that is matches the *signed hash*
	- Recipient checks the validity period to ensure that certificate has not expired
- To verify a certificate you need:
	- To know the authority's public key
		- How do we know this? Trust models (see below)
	- to **trust** the authority
PKI Trust Models
- Single CA:
	- A single CA for the entire world, all systems configured with CA's public key. All certificates obtained from CA's directory
	- Advantages:
		- Simple setup, no need to trust recommendations
	- Disadvantages:
		- No organisation is universally trusted
		- Where should it be located? Inconvenient and insecure for distant organisations to obtain certificates
		- CA has monopoly - can charge excessive fees
- Multiple CAs:
	- Every system needs a set of CA public keys
	- Advantages:
		- Local CAs are more convenient
		- competition prevents abusive pricing
	- Disadvantages:
		- Less secure than single CA model:
			- Compromise of any CA suffices to forge fraudulent certificates - if they trust each other and one is compromised, they are all compromised
			- Systems' certificate store can be manipulated by adding attacker's keys
- Configured. Delegated CAs:
	- CAs whose public keys are **configured** in a system can authorise other CAs to act as **delegated** CAs.
	- Both kinds of CAs are completely trusted to both issue certificates and to recommend delegates as trustworthy CAs.
	- Advantages: 
		- Competitive pricing
		- Convenience of local CAs
		- Systems need not be configured with all certificates
	- Disadvantages: 
		- As before
			- Compromise of any CA suffices to forge fraudulent certificates
			- Systems' certificate store can be manipulated by adding attacker's keys
Certificate Chains
- If Alice can certify Bob's PK, and Bob can certify Wilma's PK, then Alice can certify Wilma's PK etc:
	- "I, Bob certify Wilma's public key" - signed Bob
	- "I, Wilma certify Sue's public key" - signed Wilma
	- "I, Sue certify Steve's public key" - Signed Sue
	- $\therefore$ Alice can certify Steve's PK
- Can Alice trust Wilma?
	- Alice trusts Bob, who trusts Wilma
	- But Alice could think Bob is honest, but naive
- Trust is not transitive
- Recommendation levels:
	- Example
		- Alice trusts all recommendations of level 2 by Bob
		- Bob issues a recommendation of level 2 for Wilma
		- Wilma issues a recommendation of level 1 for Sue
		- Alice can trust Sue
	- level 1:
		- $P_i$: You can trust in all the certificates issued by $P_{i+1}$
	- level 2:
		- $P_i$: You can trust level 1 recommendations issued by $P_{i+1}$
	- level 3:
		- $P_i$: You can trust level 2 recommendations issued by $P_{i+1}$
	- and so on...
- In web browsers X.509 certificates include recommendation
	- this level is bounded using a field called *basic constraints/path length*
What if Private Key is Stolen?
- the certificate must be revoked
- Each CA maintains a list of revoked certificates (CRL)
In addition to trusting CAs, we have to make the following assumptions:
- The browser vendor and developers are honest
- The browser developers are competent
- The browser and the browser's certificate store have not been manipulated
Revoking the Trust in Root Certificates:
- To revoke trust in a root certificate, the certificate must be removed from the OS' and browser's trust store
Who signs the root certificate?
- Root certificates are self-signed:
	- The private key corresponding to the public key that is being certified is used to sign the issued certificate
Another issue:
- In the example where Bob goes to the judge about Alice's message, and Alice says she didn't sign it, she can say that her private key has expired, and is compromised
- This is solved with Time Stamps:
Time Stamps:
- PK certificates have an expiration date. This is to reduce the risk that a private key is compromised and abused for an indefinite amount of time
- How do you prove a signature is valid after the expiration date, on a document that was signed before the expiration date:
	- This can be solved with a trusted **Time stamp Authority** (TSA). This is frequently provided by CAs
	- TSA certifies that an electronic document has existed at a given point in time. This is done by signing a hash of the document and publishing the signed hash
### Examples:
X.509 Certificate structure
- used in IPSec, SSL/TLS, S/MIME, SSH,...
- Main problems with X.509:
	- Certificate revocation lists work only if you are online
	- Revocation of root certificates not addressed
	- CAs cannot restrict the domains on which the subordinate CAs issue certificates
	- Compromise of any one CA = complete compromise
### Common exam questions:
# Security Protocols
## Topic 14 - Security Protocols
### Key definitions:
**Security Protocols** - Employ cryptographic building blocks (encryption, hashing, digital signatures) to enable secure communication in distributed systems
**Communication protocol**: A protocol that defines the syntax, semantics, and timing of messages exchanged between parties.
**Cryptographic primitive**: A basic building block (e.g. encryption, hash functions, digital signatures) used to construct security protocols.
**Adversary (Dolev–Yao model)**: An attacker who fully controls the network, can intercept, modify, replay, and fabricate messages, and may compromise old keys.
**Honest party**: A protocol participant that follows the protocol specification and whose keys are not compromised.
**Session key**: A temporary symmetric key used to secure a single communication session.
**Freshness**: A property ensuring a key or message has not been used before.
**Secrecy**: A property ensuring the adversary does not learn the key or protected data.
**Agreement**: A property ensuring communicating parties agree on the same key and on who they are communicating with.
**Replay attack**: An attack where an adversary reuses old protocol messages to break security properties.
**Nonce**: A random value (“number used once”) used to guarantee freshness.
**Man-in-the-middle attack**: An attack where the adversary intercepts and alters communication while impersonating each party to the other.
**Authenticated key exchange**: A key exchange protocol that ensures both key secrecy and correct identification of the communicating parties.
### Core ideas:
We have RSA, AES, SHA, etc. which provide good cryptographic primitives - how can we use them to achieve secure communication in a distributed system?
Adversary model:
- able to eavesdrop on all messages sent
- able to compromise sufficiently old cryptographic keys
- able to intercept messages, send modified messages to anybody under any sender name
- able to send new messages constructed from any information available
- and may be a legitimate protocol participant (an insider), an external party (an outsider) or a combination of both
Communication Protocol:
- A distributed algorithm that is executed by two or more parties
- Specifies the syntax, semantics and synchronisation of data to be exchanged between the parties
- Security protocols use cryptographic mechanisms to achieve their security goals
Alice & Bob Notation:
- A $\rightarrow$ S : A, B
- S $\rightarrow$ A : K$_{AB}$
- A $\rightarrow$ B : K$_{AB}$, A
Symbolic Encryption Notation
- We write {m}$_k$ for a message m encrypted and authenticated with a symmetric key k
- {m}$_k$ := (Enc$_{k1}$(m), Tag$_{k0}$(Enc$_{k1}$(m))) where k$_0$, k$_1$ are keys derived from k
### Examples:
An example of a communication protocol is the Internet Protocol Stack:
- consists of ~500 protocols assigned to different layers
- Lower layers provide services for higher layers
- Application layer: HTTP, FTP, SMTP, POP,...
- Transport layer: TCP, UDP
- Internet layer: IPv4, IPv6
- Link layer: Ethernet, Token Ring, IPoAC
### Common exam questions:
## Topic 15 - SSL/TLS
### Key definitions:
**SSL** - Secure Socket Layer (deprecated protocol)
**TLS** - Transport Layer Security (successor of SSL)
### Core ideas:
RFC 2246: "SSL provides communications privacy over the internet. The protocol allows client/server applications to communicate in a way that prevents eavesdropping, tampering, or message forgery."
Goals: Confidentiality, Integrity, (mutual) Authentication
TLS consists of several subprotocols: 
- TLS Handshake Protocol
	- Initiates connection
	- Allows the server and client to authenticate each other (using RSA, DSS,...) and to exchange keys (using DH, RSA) to be used by all subprotocols
- TLS Record Protocol
	- Provides connection security for sending application data. Describes how data is compressed, authenticated and encrypted
	- Message confidentiality provided by symmetric cryptography: AES, CHACHA20,...
	- Message integrity provided by a keyed MAC: SHA256, SHA-384, or authenticated encryption (AEAD)
- Other protocols: Error recovery, renegotiating ciphers
TLS Handshake Protocol:
1. Exchange hello messages to negotiate ciphers, and algorithms, exchange random values, and check for session resumption
2. Exchange certificates to allow the server and client to authenticate themselves (in step 5)
3. Exchange cryptographic information to generate a master secret from the premaster secret and exchanged random values
4. Provide keys and security parameters to the record protocol
5. Allow the client and server to verify that their peer has calculated the same security parameters and that the handshake occurred without tampering by an attacker. This authenticates the server to the client
### Examples:
### Common exam questions:
# Networks Security
## Topic 16 - Networks Security
### Key definitions:
**Network security**: The protection of data, devices, and services as they communicate over inherently insecure networks.
**Confidentiality**: Ensuring data is only readable by authorised parties.
**Integrity**: Ensuring data is not modified in transit.
**Authentication**: Verifying the identity of communicating entities.
**Anti-replay**: Preventing attackers from reusing old packets or messages.
**Virtual Private Network (VPN)**: A secure virtual network built on top of an insecure physical network.
**Tunnel**: Encapsulation of packets inside another secure protocol.
**IPsec**: A network-layer protocol suite that secures IP packets.
**Security Association (SA)**: An agreement on cryptographic keys and algorithms for IPsec (simplex).
**DNSSEC**: Extensions to DNS that authenticate DNS responses using digital signatures.
**Network segmentation**: Dividing a network into isolated parts to limit trust and lateral movement.
**Intrusion Detection System (IDS)**: Software that detects signs of malicious activity.
**SNMP**: A protocol used for monitoring and managing network devices.
**Quality of Service (QoS)**: Techniques for managing bandwidth, delay, jitter, and packet loss.
### Core ideas:
- Networks are **insecure by design**:
    - Data on the medium is readable
    - Routers can inspect or modify packets
    - IP and Ethernet do not authenticate endpoints
- Network security aims to provide
    - Confidentiality
    - Integrity
    - Authentication
    - Anti-replay protection
- **VPNs** create a secure virtual medium on top of insecure networks:
    - Client-to-site and site-to-site use cases
    - Most valuable when securing whole networks, not just two hosts
- **TLS/DTLS-based VPNs**
    - Use TLS as a tunnel
    - Firewall-friendly (TCP 443)
    - TCP-based VPNs suffer from head-of-line blocking
    - DTLS (TLS over UDP) avoids TCP-over-TCP issues
- **IPsec** secures traffic at the network layer:
    - Encapsulates IP packets
    - Provides authentication, integrity, encryption, anti-replay
    - Tunnel mode encrypts the whole IP packet
    - Often filtered → mainly used for site-to-site VPNs
- **DNS is insecure by default**:
    - Susceptible to spoofing and cache poisoning
    - DNSSEC adds authentication via a chain of digital signatures
    - Adoption is limited due to deployment and trust-management complexity
- **Perimeter-only security is insufficient**:
    - Once attackers gain internal access, they can move laterally
    - Modern design assumes **no implicit trust**
- **Network segmentation** limits damage
    - Isolation using VLANs, ACLs, or physical separation
    - Must balance security with usability
- **IDS complements firewalls**:
    - Detects attacks via signatures and anomaly detection
    - Analyses traffic patterns, packet contents, and logs
    - Trade-off between detection and false positives
- **Network monitoring** supports security and reliability:
    - Devices report status to a central manager (SNMP)
    - Traps allow urgent alerts
- **QoS ensures reliable service**:
    - Traffic is classified using headers and ports
    - Routers prioritise traffic using queueing strategies
    - Important for latency-sensitive applications
### Examples:
### Common exam questions: