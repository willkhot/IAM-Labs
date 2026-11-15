# 🔐 IAM Labs

Identity and Access Management labs on **Microsoft Entra ID**. The course exercises are follow-alongs from what I'm studying for **SC-300**, and the labs are what I build on my own with what I learned.

## [Course Exercises: Microsoft Entra ID](entra/)

Documenting what I'm learning as I study for SC-300.

### Implement and manage identities in Microsoft Entra ID

| # | Exercise | Topics |
|---|---|---|
| 01 | [Manage Users, Groups, Licenses, and Custom Security Attributes](entra/1-identities/lab-01-manage-users-groups-licenses/) | Users, security groups, dynamic membership, group-based licensing, custom security attributes |
| 02 | [Company Branding, Entra Roles, Custom Roles, and Administrative Units](entra/1-identities/lab-02-branding-roles-admin-units/) | Sign-in branding, role assignment, role-assignable groups, custom roles, administrative units, custom domains, tenant settings |
| 03 | [External Identities: Guest Users, Cross-Tenant Access, and Collaboration Settings](entra/1-identities/lab-03-external-identities/) | Guest vs member users, B2B invitations, cross-tenant access settings, identity providers, external collaboration settings |
| 04 | [Hybrid Identity: Entra Connect and Authentication Methods](entra/1-identities/lab-04-hybrid-identity/) | Hybrid identity, Cloud Sync vs Connect Sync, password writeback, password hash sync, pass-through authentication, federation |

### Plan, implement, and manage user authentication

| # | Exercise | Topics |
|---|---|---|
| 05 | [Multifactor Authentication: Methods, Policies, and Registration](entra/2a-authentication/lab-05-multifactor-authentication/) | MFA factors, per-user MFA, authentication methods policies, registration campaign, Microsoft Authenticator, My Sign-Ins |
| 06 | [Authentication Methods: Passwordless, FIDO2, and Monitoring](entra/2a-authentication/lab-06-authentication-methods/) | Method strength, system-preferred MFA, report suspicious activity, FIDO2, Microsoft Authenticator, Windows Hello for Business, CBA, registration and usage reports |
| 07 | [Self-Service Password Reset (SSPR)](entra/2a-authentication/lab-07-self-service-password-reset/) | SSPR licensing, selected-group scope, methods required to reset, security questions, administrator policy, user reset with Authenticator |
| 08 | [Disabling Accounts, Password Protection, and Smart Lockout](entra/2a-authentication/lab-08-disable-accounts-password-protection/) | Disable accounts, revoke sessions, reset password, custom banned passwords, password protection for AD, smart lockout |

### Plan, implement, and manage Conditional Access

| # | Exercise | Topics |
|---|---|---|
| 09 | [Conditional Access: Policies, Named Locations, Terms of Use, and Authentication Strengths](entra/2b-conditional-access/lab-09-conditional-access/) | Security defaults, signals and decisions, assignments vs access controls, grant and session controls, Report-only, named locations, terms of use, authentication strengths, What If |

### Manage Microsoft Entra ID Protection and threat detection

| # | Exercise | Topics |
|---|---|---|
| 10 | [Microsoft Entra ID Protection: Risk Detections, Risk Policies, and Reports](entra/2c-identity-protection/lab-10-id-protection/) | ID Protection roles and licensing, sign-in risk vs user risk, risk detections, risk-based Conditional Access, risk remediation, risk reports |
| 11 | [Microsoft Defender for Identity: Threat Detection, Sensors, and Honeytokens](entra/2c-identity-protection/lab-11-defender-for-identity/) | On-prem AD threat detection, behavioral analytics, kill chain, Defender portal, sensor activation vs classic sensor, honeytokens |

### Implement access management for Azure resources

| # | Exercise | Topics |
|---|---|---|
| 12 | [Azure Roles and Managed Identities](entra/2d-azure-resource-access/lab-12-azure-roles-managed-identities/) | Entra roles vs Azure roles, RBAC scope, Owner, Contributor, Reader, User Access Administrator, custom roles, Global Administrator elevation, system-assigned and user-assigned managed identities |
| 13 | [Azure Key Vault: Creating a Vault, RBAC Roles, and Secrets](entra/2d-azure-resource-access/lab-13-azure-key-vault/) | Key vault creation, soft delete, purge protection, RBAC vs access policies, networking, built-in Key Vault roles, secrets, expiration dates, Bastion with Key Vault |

### Plan and implement workload identities

| # | Exercise | Topics |
|---|---|---|
| 14 | [Microsoft Defender for Cloud Apps: Cloud Discovery, App Risk, and Policies](entra/3-workload-identities/lab-14-defender-for-cloud-apps/) | CASB, shadow IT, connectors, automatic log upload, log collectors, snapshot reports, custom log parser, app risk scores, sanctioned vs unsanctioned apps, user and IP investigation, policy templates |
| 15 | [App Registration in Microsoft Entra ID](entra/3-workload-identities/lab-15-app-registration/) | App admin roles, application proxy, application objects vs service principals, multitenant consent flow, registering an app, credentials, optional claims, delegated vs application permissions, admin consent, app roles, manifest, owners |
| 16 | [Enterprise Apps in Microsoft Entra ID](entra/3-workload-identities/lab-16-enterprise-apps/) | Application ID vs object ID, sign-in/assignment/visibility settings, user assignment with app roles, user and admin consent, permission classifications, application proxy and private network connector, App Gallery, SSO and provisioning, app collections |

## [Labs](labs/)

Labs I build on my own from what I learned in the course exercises.

### Implement and manage hybrid identity

| # | Lab | Topics |
|---|---|---|
| 01 | [Building a Hybrid Identity Lab: Active Directory on Hyper-V (Part 1)](labs/hybrid-identity/lab-01-hybrid-identity-ad-entra-connect/) | Hyper-V, Windows Server 2022, AD DS, DNS, new forest, domain join |
| 02 | [Building a Hybrid Identity Lab: Entra Connect Sync with Password Hash Sync (Part 2)](labs/hybrid-identity/lab-02-entra-connect-sync-phs/) | Entra Connect Sync, password hash sync, OU filtering, UPN suffixes, source anchor, Seamless SSO, password and group writeback |

### Plan and automate identity governance: privileged access

| # | Lab | Topics |
|---|---|---|
| 03 | [Zero Trust Privileged Access: Entra PIM + Phishing-Resistant MFA](labs/privileged-access/lab-03-pim-phishing-resistant-mfa/) | PIM just-in-time Global Admin, authentication context, Conditional Access, authentication strength, device-bound passkey, break glass, log validation |

> For IAM on AWS, see [Introduction to AWS IAM](https://github.com/willkhot/Cloud-Labs/tree/main/aws/lab-01-intro-to-iam) in my Cloud Labs.

## What I've Been Learning

**Identity (Microsoft Entra ID)**
- Creating and managing users and groups, including groups that add people automatically based on a rule
- Giving out licenses to a whole group instead of one person at a time
- Tagging users with custom attributes, like a security clearance level

## Author

**Will Khotsyphom**

[![GitHub](https://img.shields.io/badge/GitHub-willkhot-181717?logo=github)](https://github.com/willkhot)

## Security Note

Screenshots in this repository are sanitized. Tenant domains and IDs, user principal names, object IDs, emails, account names, device names and IP addresses are redacted or replaced with placeholders. The users and company shown (Bam Co.) are fictional test accounts in a personal lab tenant.
