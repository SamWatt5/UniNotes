# Chapter 1 of "[Introduction to Cryptography](https://link.springer.com/book/10.1007%2F978-3-662-47974-2)"
## Abstract
Cryptography is the science of keeping secrets secret. Assume a sender, referred to here and in what follows as Alice (as is commonly used), wants to send a message m to a receiver, referred to as Bob. She uses an insecure communication channel. For example, the channel could be a computer network or a telephone line. There is a problem if the message contains confidential information. The message could be intercepted and read by an eavesdropper. Or, even worse, the adversary, as usual referred to here as Eve, might be able to modify the message during transmission in such a way that the legitimate recipient Bob does not detect the manipulation. One objective of cryptography is to provide methods for preventing such attacks. Other objectives are discussed in Section 1.2.
## Headings
### 1.1 Encryption and Secrecy
### 1.2 The objectives of Cryptography
### 1.3 Attacks
### 1.4 Cryptographic Protocols
### 1.5 Provable Security
## Key Words
# Chapter 5 of "[The basics of information security](http://www.sciencedirect.com.libezproxy.dundee.ac.uk/science/book/9780128007440)"
## Abstract
In this chapter, we discuss the use of cryptography. We go over the history of such tools, from very simple [substitution ciphers](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/substitution-cipher "Learn more about substitution ciphers from ScienceDirect's AI-generated Topic Pages") to the fairly complex electromechanical machines that were used just before the invention of the first modern computing systems, and how they form the basis for many of our modern algorithms. We cover the three main categories of [cryptographic algorithms](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/cryptographic-algorithm "Learn more about cryptographic algorithms from ScienceDirect's AI-generated Topic Pages"): [symmetric key cryptography](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/symmetric-key-cryptography "Learn more about symmetric key cryptography from ScienceDirect's AI-generated Topic Pages"), also known as [private key cryptography](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/private-key-cryptography "Learn more about private key cryptography from ScienceDirect's AI-generated Topic Pages"); asymmetric [key cryptography](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/key-cryptography "Learn more about key cryptography from ScienceDirect's AI-generated Topic Pages"); and [hash functions](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/hash-function "Learn more about hash functions from ScienceDirect's AI-generated Topic Pages"). We also talk about digital signatures that can be used to ensure that data has not been altered, and certificates that allow us to link a [public key](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/public-key "Learn more about public key from ScienceDirect's AI-generated Topic Pages") to a particular identity. In addition, we cover the mechanisms we use to protect [data at rest](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/data-at-rest "Learn more about data at rest from ScienceDirect's AI-generated Topic Pages"), in motion, and, to a certain extent, in use.
## Headings
### Introduction [70](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0010)
### History [70](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0015)
Caesar cipher [71](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0020)  
Cryptographic machines [71](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0025)
### More advanced [74](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0030)
### Additional resources [75](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0035)
Kerckhoffs’ principle [75](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0040)
### Modern cryptographic tools 75
#### Symmetric versus asymmetric cryptography [76](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0050)
Symmetric cryptography [76](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0055)  
Asymmetric cryptography [78](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0070)
### More advanced 79
Hash functions [79](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0085)  
Digital signatures [80](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0090)  
Certificates [80](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0095)
### Protecting data at rest, in motion, and in use [81](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0100)
#### Protecting data at rest [81](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0105)
Data security [82](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0110)  
Physical security [83](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0115)
### Alert! [83](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0120)
#### Protecting data in motion [84](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0125)
Protecting the data itself [84](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0130)  
Protecting the connection [84](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0135)
#### Protecting data in use [85](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0140)
### Cryptography in the real world [85](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0145)
### Summary [86](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0150)
### Exercises [87](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0155)
### References 87
## Conclusion
## Keywords
Asymmetric
Caesar cipher
certificates
cryptographic machines
cryptography
data at rest
data in motion
data in use
digital signatures
hash functions
Kerckhoffs’ principle
ROT13
symmetric
# Chapter 5 of "[Security Engineering](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c05.pdf)" Second Edition