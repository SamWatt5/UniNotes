# Threats, Risks and Attacks
## Understanding Risk
To understand risk, let's look at earthquakes risk assessment:
![[Pasted image 20250928183345.png]]
http://www.seismo.ethz.ch/en/knowledge/seismic-risk-switzerland/
Risk is composed of a thread (earthquake hazard) and impact (damage to buildings).

**How can you reduce your personal risk?**
- Live where there are no earthquakes
- Live where the ground is stable
- Build buildings of little value
- Build strong buildings
Alternative options:
- **Accept** the risk
- **Transfer** the risk - insurance

## What must we know to assess a system's security
- What are we protecting? (asset)
- Who is the attacker? (threat agent)
- What are the threats?
- What are the vulnerabilities?
- What are effective defence mechanisms?
### Definitions
**Threat**: Potential cause of an unwanted event that may harm assets
**Vulnerability**: A characteristic of a system that can be exploited by a threat
**Countermeasure**: Means to deflect, deter, or deny attacks to threatened assets
**Risk**: Possibility to suffer harm or loss. A function of loss associated with an event and probability that event occurs.

Working definition for risk associated with vulnerabilities:$$\text{risk}=(\text{impact to asset from exploit of vulnerability})\times(\text{probability of occurence})$$
![[Pasted image 20250928184348.png]]
## Risk Assessment
1. Identify assets, threat agents, and threats to assess
2. Identify vulnerabilities that can be exploited
3. Measure probability of occurence and impact (potential loss) of exploits

### Example
Risk resulting from a vulnerability and its exploit:
$$\text{impact}\times\text{prob. of occurence}$$e.g. $£20,000\times50\%/\text{year}=£10,000/\text{year}$
## Threat Agents: Skills, Motives and Opportunity (Size matters, too)
1. Identify relevant threat agents, e.g.
	- External attacker vs inside attacker
	- Script kiddies vs organised criminals
	- Competitors vs nation states
	- Accidental vs intentional actors
2. Identify threat agents' skills and motives
3. Identify threat agents' opportunity and group size
### Skills and Motives
![[Pasted image 20250928185449.png]]
### Opportunity and Size
![[Pasted image 20250928185528.png]]
## Identifying Vulnerabilities
- Finding vulnerabilities is difficult!
- To get some data, look at open-source bugs:
- Average life time of Linux kernel security bug discovered over the last years: 5 years (https://outflux.net/blog/archives/2016/10/18/security-bug-lifetime/)
- Major companies sponsor competitions (e.g., Pwn2Own, https://cansecwest.com/) to  
- find bugs, and directly reward those who report vulnerabilities to them.  
	- For example: at Pwn2Own 2016, $460,000 were awarded in total for 21 vulnerabilities found in Chrome, Edge, and Safari
- Other companies (e.g., https://zerodium.com/) buy vulnerabilities for much larger amounts and sell that information to governments and other entities willing to buy information on undisclosed vulnerabilities
## OWASP risk rating methodology
![[Pasted image 20250928212801.png]]
### Example
![[Pasted image 20250928212840.png]]
# Dealing with Risk
## Information Security
We can take two views of security:
1. Minimising the risk of abuse
	- most commonly taken for system administration
2. Building a system that meets a specification
	- taken for construction of secure systems or when certification requires it
## Risk Mitigation
1. Prioritise the risks
2. Identify countermeasures
3. Evaluate the countermeasures:
	- How well do they reduce the risk?
	- How expensive are they?
	- What trade-offs and new risks do they bring?
4. Implement countermeasures
(and stay within a given budget)
## Security as Policy Compliance
1. Specify what the system should do
2. Design and implement a system that meets the specification in the intended environment
3. Security specification states what system behaviours are acceptable/unacceptable
Example:
- Any user may read a blog, only authenticated users may post comments
### What is the intended environment?
- For software engineering, the environment consists of typical users of a system and other systems.
- For security, the environment additionally contains the **adversary** (aka. threat agent)
- The system should work even when the environment is at its worst
### Example: Mobile Communication
- 8 billion registered SIM cards, 5 billion users
- 5G provides **higher network throughput**, support for **devices moving at high speed, IoT devices**
- **Many security requirements**: authentication, confidentiality, integrity, availability, privacy,...
![[Pasted image 20250928213735.png]]
(Some) security requirements:
- mutual authentication between UE and HN
- confidential communication between UE and SN
### Specifying What The System Should Do
![[Pasted image 20250928214012.png]]
### Intended Environment (Threat Model)
**Adversary**
- Has full control over the communication network
- May eavesdrop on, inject, block, modify messages, impersonate users
- May compromise cryptographic session keys, long-term keys

**Specification**: What is the system (not) supposed to do?
- Given by a *security policy*, often formulated to achieve standard security properties (CIA)
- **Examples**: 
	- 5G communication: mutual authentication between UE and HN
	- Online banking: Transfer of funds required user authentication
**Implementation**: How does it do it?
- Consists of *security mechanism* to enforce the security policy.
- **Examples**:
	- Digital signatures
	- Password authentication
**Correctness**: Does it really work? (Is it "secure" in the intended environment?)
- Provides assurance by demonstrating *compliance with the security policy*
- **Examples**:
	- Testing
	- Formal verification





