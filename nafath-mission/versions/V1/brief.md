Version: NAFATH-V1
Your track: Software

## Overview
The NAFATH-V1 secure national digital login service integrates six critical IT domains to deliver a unified, resilient authentication ecosystem. At its core, the software architecture establishes identity trust, while mobile client components manage application sandboxing and secure user privileges locally. This authentication data traverses protected networking infrastructures designed to shield metadata from external interception. Concurrently, rigorous cybersecurity protocols mitigate advanced identity theft and impersonation attacks. The entire operation generates sensitive logs managed under strict data governance frameworks to ensure complete alignment with sovereign regulatory standards. Finally, the central core relies heavily on the specific engineering differences between OAuth 2.0 and OpenID Connect to govern user authentication.

## Software
OAuth 2.0 is an authorization framework designed exclusively for delegated access to resources using tokens, not user authentication. OpenID Connect (OIDC) is an identity layer built on top of OAuth 2.0 specifically designed for secure user login. OIDC introduces an ID token alongside the access token, enabling the system to verify the citizen's identity. Thus, OIDC handles authentication, while OAuth 2.0 governs authorization boundaries.

Resource: RFC 6749 - The OAuth 2.0 Authorization Framework - https://ietf.org

## AI
Deploying an automated AI model to flag suspicious logins introduces deployment and operational risks. According to the NIST AI Risk Management Framework, the authority must manage risks related to systemic bias, lack of explainability, and false positives that lock out valid citizens. Furthermore, the model faces security risks like adversarial evasion attacks and data poisoning, which must be rigorously mitigated before live deployment.

Resource: NIST AI Risk Management Framework (AI RMF 1.0) - https://nist.gov

## Mobile
Android’s runtime permission model restricts the login app by isolating it within a secure sandbox, preventing automatic access to sensitive device resources. The app must explicitly request permissions from the user at runtime, rather than during installation, the exact moment the resource is needed. This applies to dangerous permissions like precise location, camera for biometric scans, or device storage access.

Resource: Android Developers Documentation - Request runtime permissions - https://android.com


## Networking
DNS over HTTPS (DoH) encrypts domain name lookups inside standard HTTPS traffic. For NAFATH-V1 users, DoH protects against eavesdropping, spoofing, and local internet service provider tracking of their lookups. However, DoH does not protect or hide the final destination IP address of the government website, nor does it secure the actual payload data if the endpoint server itself is compromised.

Resource: RFC 8484 - DNS Queries over HTTPS (DoH) - https://ietf.org

## Cybersecurity
An authentication method is phishing-resistant if it cryptographically binds the authentication credential to the specific origin domain of the service. Multi-factor authentication (MFA) methods like FIDO2/WebAuthn hardware keys and passkeys qualify because they prevent credential interception. Conversely, SMS one-time passwords, voice codes, and standard mobile push notifications do not qualify because users can be tricked into revealing them.

Resource: NIST SP 800-63B - Digital Identity Guidelines: Authentication and Lifecycle Management - https://nist.gov

## Data
Under Oman's Personal Data Protection Law, the authority faces strict statutory obligations when processing citizens' data. It must obtain explicit user consent before collection and process data transparently for specified legal purposes. The authority must implement robust data security measures, notify regulators of data breaches, maintain accurate processing logs, and guarantee citizens their rights to data correction, erasure, and access.

Resource: Oman Royal Decree No. 6/2022 Promulgating the Personal Data Protection Law - https://mjla.gov.om


## Misconception in My Track
A common wrong belief in software engineering is that successful validation of an OAuth 2.0 access token is sufficient proof of user authentication. In reality, an access token only proves that a client has been granted delegated access to specific resources, not who the user is or when they logged in. This is explicitly proven in RFC 6749, Section 1.0, under the definition of "Authorization Grant", which states it is a credential representing the resource owner's authorization, distinct from end-user identity verification.

## Open Question
I would next verify how the NAFATH-V1 service handles identity provider session timeouts when a citizen simultaneously accesses multiple cross-departmental government applications.

