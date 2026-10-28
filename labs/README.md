# IAM Labs

The actual labs. These aren't follow-alongs from a course. I pick a scenario, build it myself using what I learned in the course exercises, and write up what I did.

| # | Lab | Topics | Builds on |
|---|---|---|---|
| 01 | [Building a Hybrid Identity Lab: Active Directory on Hyper-V (Part 1)](lab-01-hybrid-identity-ad-entra-connect/) | Hyper-V, Windows Server 2022, AD DS, DNS, new forest, domain join | [Hybrid Identity exercise](../entra/lab-04-hybrid-identity/) |
| 02 | [Building a Hybrid Identity Lab: Entra Connect Sync with Password Hash Sync (Part 2)](lab-02-entra-connect-sync-phs/) | Entra Connect Sync, password hash sync, OU filtering, UPN suffixes, source anchor, Seamless SSO, password and group writeback | [Lab 01](lab-01-hybrid-identity-ad-entra-connect/), [Hybrid Identity exercise](../entra/lab-04-hybrid-identity/), [SSPR](../entra/lab-07-self-service-password-reset/) |
| 03 | [Zero Trust Privileged Access: Entra PIM + Phishing-Resistant MFA](lab-03-pim-phishing-resistant-mfa/) | PIM just-in-time Global Admin, authentication context, Conditional Access, authentication strength, device-bound passkey, break glass, log validation | [MFA](../entra/lab-05-multifactor-authentication/), [Authentication Methods](../entra/lab-06-authentication-methods/) |

[← Back to IAM Labs](../)
