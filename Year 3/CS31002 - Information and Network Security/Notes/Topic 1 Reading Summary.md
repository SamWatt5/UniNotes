# Introduction
As the adoption of technology constantly increases, so does the need for **Information Security**. Every day, you use your phone to check emails, bank balance, track our exercise, etc. Although this technology allows us to be more productive, so to does it increase the damage if this relationship was to be breached. If something were to occur, we could have our bank accounts drained, our information stolen, and more! 
# What is Security
According to US Law [^1], information security is defined as *"Protecting information and information systems from unauthorized access, use, disclosure, disruption, modification, or destruction,"*. This essentially means we want to protect our data and systems assets from those who would seek to misuse it.
In a general sense, security means protecting our assets. This could mean protecting them from attackers invading our networks, viruses/worms, natural disasters, adverse environmental conditions, power failures, theft or vandalism, or other undesirable states. Ultimately, we will attempt to secure ourselves against the most likely forms of attack, to the best extent we reasonably can, given our environment.
When we look at what it is exactly that we want to secure, it could be a broad range of assets. It could be physical items, such as stock, or computer hardware, or software, source code and data. Additionally we must also protect the people involved in our operations. 
When designing our security system, it is also critical that we factor in the usability of the asset, once its secured. As we increase the level of security, we usually decrease the level of productivity. The goal of a security plan is to find the balance between protection, usability and cost. Additionally we must also factor in how the level of security relates to the value of the item being secured.

[^1]: US Government, Legal Information Institute, Title 44, Chapter 35, Subchapter 111, y3542, Cornell University Law School, <www.law.cornell.edu/uscode/44/3542.html>

# When are we secure?
It is difficult to define exactly *when* we are *secure*. Is it when our systems are properly patched? Is it when we use a strong password? If we disconnect from the internet entirely? From a certain point of view, the answer will always be "no", so the real question is are we *reasonably* secure?
It is very difficult to ask when we are truly secure, instead, however, we can flip the question around. Defining when we are insecure is a much easier task:
- Not patching our systems or not patching quickly enough
- Using weak passwords such as "password" or "12345678"
- Downloading infected programs from the internet
- Opening dangerous email attachments from unknown senders
- Using wireless networks without encryption that can be monitored by anyone
Once we are able to point out these issues, we can take steps to mitigate them. Although we may never be *completely secure* we can take steps in the right direction.

# Compliance
Compliance is a key aspect of any security program and should be coordinated across the organization. The bodies of law that define standards for security vary a lot from one industry to another and from one country to another. This is clear looking at the difference between data privacy laws in the US and the EU.
Some bodies of law or regulations do make an attempt to define what secure is, or at least some of the steps we should take. We have the *Payment Card Industry Data Security Standard (PCI DSS)* for companies that process credit card payments, the *Health Insurance Portability and Accountability Act of 1996 (HIPAA)* for organizations that handle health care and patient records, the *Federal Information Security Management Act (FISMA)* that defines security standards for many federal agencies in the US, and a host of others. Whether these standards are effective or not is a source of discussion, but following the security standards defined for the industry in which we are operation is generally advisable, if not mandated.

# Models for Discussing Security
When we discuss security issues, it is often helpful to have a model or framework that we can use as a foundation or a baseline. This gives us a consistent set of terminology and concepts that we, as security professionals, ca refer to when security issues arise.
## The Confidentiality, Integrity, and availability triad
Three of the primary concepts in information security are confidentiality, integrity, and availability, commonly known as the confidentiality, integrity, and availability (*CIA*) triad. The CIA triad gives us a model by which we can think about and discuss security concepts, ad tends to be very focused on security, as it pertains to data.![[Pasted image 20250923113359.png]]
### Confidentiality
Confidentiality is a concept similar to, but not the same as privacy. It is a necessary component of privacy and refers to our ability to protect our data from those who are not authorized to view it. Confidentiality is a concept that can be implemented at many levels of a process.
For example, if we consider the case of a person withdrawing money from an ATM, the person will likely seek to maintain the confidentiality of the PIN that allows him, with his card, to withdraw funds.  Additionally, the owner of the ATM will hopefully maintain the confidentiality of the account number, balance, and any other information needed to communicate to the bank from which the funds are being withdrawn. The bank will maintain the confidentiality of the transaction with the ATM and the balance change in the accound after the funds have been withdrawn. If at any point the transaction confidentiality is compromised, the results could be bad for the individual, the owner of the ATM, and the bank, potentially resulting in what is known in the information security field as a *breach*.
Confidentiality can be compromised by the loss of a laptop containing data, a person looking over our shoulder while we type a password, an email attachment being sent to the wrong person, an attacker penetrating our systems, or similar issues.

### Integrity
Integrity refers to the ability to prevent our data from being changed in an unauthorised or undesirable manner. This could mean the unauthorised change or deletion of our data or portions of our data, or it could mean an authorised, but not desirable, change or deletion of our data. To maintain integrity, we not only need to have the means to prevent unauthorised changes to our data, but also need to be able to reverse authorised changed that need to be undone.
An example of this is the file systems on modern operating systems, such as Windows or Linux. To stop unauthorised changes, such systems often implement permissions that restrict what actions an authorised user can perform on a given file. Additionally, some such systems, and many applications, such as databases, can allow unto undo or roll back changes that are undesirable.
Integrity is particularly important when we are discussing the data that provides the foundation for other decisions. If an attacker were to alter the data that contained the results of medical tests, we might see the wrong treatment prescribed.
### Availability
Finally, availability refers to the ability to access our data when we need it. Loss of availability can refer to a wide variety of breaks anywhere in the chain that allows us access to our data. Such issues can result from power loss, operation system or application problems, network attacks, compromise of a system, or other problems. When such issues are caused by an outside party, such as an attacker, they are commonly referred to as a *Denial of Service* (DoS) attack.

## The Parkerian Hexad
The Parkerian hexad, named for Donn Parker and introduced in his bok *Fighting Computer Crime*, provides us with a somewhat more complex variation of the classic CIA triad. Where the CIA triad consists of confidentiality, integrity and availability, the Parkerian hexad consists of these three principles, as well as possession or control, authenticity, and utility, for a total of six principles.

### Differences and benefits
The Parkerian hexad encompasses the CIA triad, but as Parker describes integrity, he doesn't account for authorised, but incorrect, modification of data and instead focuses on the state of the data itself in the sense of completeness.
### Possession or control
Possession or control refers to the physical disposition of the media on which the data is stored. This enables us, without involving other factors such as availability, to discuss our loss of the data in its physical medium. For example, an encrypted hard drive could end up in the wrong hands, and this is a possession problem, not a confidentiality problem.
### Authenticity
Authenticity allows us to talk about the proper attribution as to the owner or creator of the data in question. For example, if we send an email with an altered message, so as to appear to have come from a different email address than the one from which it was actually sent, we would be violating the authenticity of the email. Authenticity can be enforced through the use of digital signatures. 
### Utility
Utility refers to how useful the data is to us. Utility is the only principle of the Parkerian hexad that is not binary in nature; we can have a variety of degrees of utility, depending on the data and its format. This is a fairly abstract concept, but it does prove useful in discussing certain situations in the security world. For example, an encrypted hard drive in an attackers hands would be not as *useful* to them as an unencrypted hard drive.

# Attacks
We may face attacks from a wide range of approaches. When we look at what makes up an attack, we can break it down according to the type of attack that it represents, the rist the attack represents, and the controls we might use to mitigate it.
## Types of Attack Payloads
When we look at the types of attacks we might face, we can generally place them into one of four categories:
