# Chapter 12
## Abstract
In this chapter, we consider the various ways in which we might secure our applications. We go over the vulnerabilities common to the software development process, including [buffer overflows](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/buffer-overflow "Learn more about buffer overflows from ScienceDirect's AI-generated Topic Pages"), race conditions, input validation attacks, [authentication attacks](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/authentication-attack "Learn more about authentication attacks from ScienceDirect's AI-generated Topic Pages"), [authorization attacks](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/authorization-attack "Learn more about authorization attacks from ScienceDirect's AI-generated Topic Pages"), and [cryptographic attacks](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/cryptographic-attack "Learn more about cryptographic attacks from ScienceDirect's AI-generated Topic Pages"), and how we might mitigate these by following secure coding guidelines. We talk about Web security, the areas of concern on both the client and server sides of the technology. We introduce database security and cover protocol issues, [unauthenticated access](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/unauthenticated-access "Learn more about unauthenticated access from ScienceDirect's AI-generated Topic Pages"), [arbitrary code execution](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/arbitrary-code-execution "Learn more about arbitrary code execution from ScienceDirect's AI-generated Topic Pages"), and [privilege escalation](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/privilege-escalation "Learn more about privilege escalation from ScienceDirect's AI-generated Topic Pages") and the measures we might take to mitigate them. Lastly, we examine security tools from an application perspective, including sniffers such as [Wireshark](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/wireshark "Learn more about Wireshark from ScienceDirect's AI-generated Topic Pages"), fuzzing tools including some developed by Microsoft, and Web application analysis tools such as [Burp Suite](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/burp-suite "Learn more about Burp Suite from ScienceDirect's AI-generated Topic Pages") in order to better secure our applications.
## Headings
### Introduction [190](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0010)
### The TJX breach [190](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0015)
### Software development vulnerabilities [191](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0020)
### Additional resources [191](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0025)
Buffer overflows [192](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0030)  
Race conditions [192](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0035)  
Input validation attacks [193](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0040)  
Authentication attacks 193  
Authorization attacks [194](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0050)  
Cryptographic attacks [194](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0055)
### Web security [195](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0060)
#### Client-side attacks [195](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0065)
Cross-site scripting [195](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0070)
### Alert! [196](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0075)
### More advanced [196](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0095)
#### Server-side attacks [197](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0100)
Lack of input validation [197](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0105)  
Improper or inadequate permissions [198](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0110)  
Extraneous files [198](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0115)
### Database security [198](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0120)
Protocol issues [199](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0125)  
Unauthenticated access [200](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0130)  
Arbitrary code execution [200](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0135)  
Privilege escalation [201](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0140)
### Additional resources [201](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0145)
### Application security tools [202](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0150)
Sniffers [202](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0155)
#### Web application analysis tools [202](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0160)
Nikto and Wikto [203](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0165)
### Alert! [203](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0175)
Burp Suite [204](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0180)
Fuzzers [204](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000014#s0185)
### More advanced 205
### Application security in the real world 206
### Summary 207
### Exercises 208
### References 208
## Conclusion
A number of vulnerabilities are common to the software development process, across many of the platforms on which we might be developing or implementing our solution. We may encounter buffer overflows, race conditions, input validation attacks, authentication attacks, authorization attacks, and cryptographic attacks, just to name a few. Although such issues are very common, most of them can be resolved with relative ease by following secure coding guidelines, either those internal to our organizations, or from [external sources](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/external-source "Learn more about external sources from ScienceDirect's AI-generated Topic Pages") such as NIST, [CERT](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/topics/computer-science/computer-emergency-response-team "Learn more about CERT from ScienceDirect's AI-generated Topic Pages"), or the Build Security in Software Assurance Initiative (BSI) from the US Department of Homeland Security.[4](https://www-sciencedirect-com.libezproxy.dundee.ac.uk/science/chapter/monograph/pii/B9780128007440000129#fn4)

In terms of Web security, the areas of concern break out into client-side issues and server-side issues. Client-side issues involve attacks against the client software we are running, or the people using the software. We can help mitigate these by ensuring that we are on the most current version of the software and associated patches, and sometimes by adding extra security tools or plug-ins. On the other side, we have attacks that are directly against the Web server itself. Such attacks often take advantage of lack of strict permissions, lack of input validation, and leftover files from development or troubleshooting efforts. Fixing such issues requires careful scrutiny by both developers and security personnel.

Database security is a large concern for almost any Internet-facing application. The main categories of database security concerns are protocol issues, unauthenticated access, arbitrary code execution, and privilege escalation. Many of these problems can be mitigated by following secure coding practices, keeping up-to-date on our software versions and patches, and following the principle of least privilege.

There are a number of application security tools that we can use in our efforts to render our applications more able to resist attack. As with network and host security, we can put sniffers to use in examining what enters and exits our applications in terms of network data. We can also use reverse engineering tools to examine how existing applications operate and to determine what weaknesses we might have that a skilled reverse engineer could exploit. In addition, we can make use of fuzzing tools and Web application analysis tools in order to locate vulnerabilities, whether known or unknown.
## Keywords
Application security
authentication
authorization
buffer overflow
Burp Suite
cryptographic attack
database security
fuzzing
input validation
protocol
race condition
Web security
Wireshark