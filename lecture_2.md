# Lecture 2

## Threat Model

- Thread Model defines **Security Goals**:
  - Assets: _What are we trying to protect from_
  - Attackers: _Whom are we trying to protect from_
- Must understand the value of the assets to decide the budget for protection
- Goal: preserve **confidentiality**, **integrity**, and **availability** (C.I.A.) of the system

## Assets (C.I.A)

### Confidentiality (Secrecy)

- Prevention of unauthorized access to the information
- Example
  - Alice wants to send message to Bob
  - Zurg the Evil **copies** the content of the message

### Integrity (Authenticity)

- Integrity: Prevention of unauthorized change
  - Example
    - Increase bank balance without depositing money
    - Getting snack without paying
    - Zurg the Evil **modifies** the content of the message
- Authenticity: Identification and assurance of origin
  - Example
    - Getting money from one's bank account by using their identity
    - Zurg the Evil sends a message to Bob by impersonating Alice

### Availability

- Preventiont of unathorized denial of service to authorized users
  - Unauthorized parties can’t prevent authorized users from accessing system
- Example
  - Putting superglue in the ATM card slot
  - Network denial of service attacks (e.g., packet floods)
  - Zurg the Evil floods the message service and causes the service to deny Alice's request

### Privacy

- A person's right or expectation to control the disclosure of their personal information, including activity metadata
- Secrecy vs Privacy
  - Secrecy is about explicitly hiding information
  - Privacy is about not being observed/monitored

### Vulnerability

- Weaknesses that could be exploited to cause damage to assets
  - Default password left intact (“password”)
  - Implementation flaws in software
  - Debug interface left open to network
  - Cryptography based on weak keys
- In particular, look to assumptions in system

## Attackers / Adversaries

- Trusted Computing Base
  - Set of systems/components/people/entities that your security depends on
- Trust / Security Boundary
  - Perimeter around components of same trust level
- Attack Surface
  - Set of interaction points across a security boundary
  - For example, parts of my system handling input from or interacting with less trusted and potentially malicious entities

## Risk Assessments

1. Start by understanding system requirements
   - _What is the security boundary_
2. Identify assets and attackers
   - _What is the value_
   - _From who it needs to be protected from_
3. Establish security requirements
   - An attacker must not be able to compromise the C.I.A. of ...
4. Evaluate system design
   - _What are the different components in the system_
     - how do they communicate
     - how do they store data
   - Draw a block diagram
     - Indicate security boundaries
5. Identify threats and classify risks
   - Possible ways in which attackers could exploit vulnerabilities in system design or implementation to compromise the assets
   - determine likelihood and impact and convert it to a **risk score**
6. Address identified risks
   - Avoid: Remove the component that creates the risk
   - Mitigate: Add measures that decrease likelihood or impact (e.g. insurance)
   - Transfer: Make it someone else’s problem
   - Accept: Do nothing

## Key Notes

1. Your threat model is your problem scope.
2. Attackers **don’t care** about your threat model.
3. Just because an asset or an attacker are outside your threat model, it does not mean that they do not exist.
