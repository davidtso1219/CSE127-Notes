# Lecture 1

## Two Computer Sucurity Models

1. Binary model (secure / insecure)
   - Assume adversary limitations X and define security policy Y
   - if Y cannot be violated without needing X then system is secure, else insecure
   - keywords: proof of security, secure by design, trustworthy system
   - example: perfect substitution cipher
2. Risk management model (more secure / less secure)
   - try to identify most significant risks to security and minimize them
   - keywords: risk, mitigation, defense, resilience
   - example: concrete barricades

## Key Meta Issues in Security

- Policy
  - _What is a bad thing?_
  - remarkably to define even for known threats
  - even harder for unknown threats
- Assets, Risks, and Threats
  - Assets: what you want to protect
  - Threats: actions to cause damage, harm, or loss
  - Risk: likelihood for something bad happening
- Value
  - _What is the cost if a bad thing happens_
  - _What is the cost to prevent the bad thing_
- Protection
  - The mechanisms to protect resources against threats
  - Examples:
    - Cryptographic protection of data
    - Software/Communication Guards
    - User Interface Design (protect users from their own limitations)
- Deterrence
  - expectations of future cost from doing something bad
- Identity & Reputation
  - Identity: an abstract idea of the distinct personality of an individual
  - Identifier: a concrete object that assert one's reputation
  - Reputation: a specific characteristic or trait ascribed to a person or thing

## Due Diligence and Trust

1. Due Diligence
   - Work to acquire multiple independent pieces of evidence establishing identity/reputation linkage through direct experience instead of a third party
2. Allows cheap form of due-diligence: third-party attestation

## Key Notes

1. Computer security is not about functionality but about how some implementation of functionality behaves in the presence of an adversary.
