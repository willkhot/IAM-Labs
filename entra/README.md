# Microsoft Entra ID Labs

Identity and Access Management labs on **Microsoft Entra ID**. These labs document what I'm learning as I study for the **SC-300: Microsoft Identity and Access Administrator** certification.

## Implement and manage identities in Microsoft Entra ID

| # | Lab | Topics |
|---|---|---|
| 01 | [Manage Users, Groups, Licenses, and Custom Security Attributes](1-identities/lab-01-manage-users-groups-licenses/) | Users, security groups, dynamic membership, group-based licensing, custom security attributes |
| 02 | [Company Branding, Entra Roles, Custom Roles, and Administrative Units](1-identities/lab-02-branding-roles-admin-units/) | Sign-in branding, role assignment, role-assignable groups, custom roles, administrative units, custom domains, tenant settings |
| 03 | [External Identities: Guest Users, Cross-Tenant Access, and Collaboration Settings](1-identities/lab-03-external-identities/) | Guest vs member users, B2B invitations, cross-tenant access settings, identity providers, external collaboration settings |
| 04 | [Hybrid Identity: Entra Connect and Authentication Methods](1-identities/lab-04-hybrid-identity/) | Hybrid identity, Cloud Sync vs Connect Sync, password writeback, password hash sync, pass-through authentication, federation |

## Plan, implement, and manage user authentication

| # | Lab | Topics |
|---|---|---|
| 05 | [Multifactor Authentication: Methods, Policies, and Registration](2a-authentication/lab-05-multifactor-authentication/) | MFA factors, per-user MFA, authentication methods policies, registration campaign, Microsoft Authenticator, My Sign-Ins |
| 06 | [Authentication Methods: Passwordless, FIDO2, and Monitoring](2a-authentication/lab-06-authentication-methods/) | Method strength, system-preferred MFA, report suspicious activity, FIDO2, Microsoft Authenticator, Windows Hello for Business, CBA, registration and usage reports |
| 07 | [Self-Service Password Reset (SSPR)](2a-authentication/lab-07-self-service-password-reset/) | SSPR licensing, selected-group scope, methods required to reset, security questions, administrator policy, user reset with Authenticator |
| 08 | [Disabling Accounts, Password Protection, and Smart Lockout](2a-authentication/lab-08-disable-accounts-password-protection/) | Disable accounts, revoke sessions, reset password, custom banned passwords, password protection for AD, smart lockout |

## Plan, implement, and manage Conditional Access

| # | Lab | Topics |
|---|---|---|
| 09 | [Conditional Access: Policies, Named Locations, Terms of Use, and Authentication Strengths](2b-conditional-access/lab-09-conditional-access/) | Security defaults, signals and decisions, assignments vs access controls, grant and session controls, Report-only, named locations, terms of use, authentication strengths, What If |

## Manage Microsoft Entra ID Protection and threat detection

| # | Lab | Topics |
|---|---|---|
| 10 | [Microsoft Entra ID Protection: Risk Detections, Risk Policies, and Reports](2c-identity-protection/lab-10-id-protection/) | ID Protection roles and licensing, sign-in risk vs user risk, risk detections, risk-based Conditional Access, risk remediation, risk reports |
| 11 | [Microsoft Defender for Identity: Threat Detection, Sensors, and Honeytokens](2c-identity-protection/lab-11-defender-for-identity/) | On-prem AD threat detection, behavioral analytics, kill chain, Defender portal, sensor activation vs classic sensor, honeytokens |

## Implement access management for Azure resources

| # | Lab | Topics |
|---|---|---|
| 12 | [Azure Roles and Managed Identities](2d-azure-resource-access/lab-12-azure-roles-managed-identities/) | Entra roles vs Azure roles, RBAC scope, Owner, Contributor, Reader, User Access Administrator, custom roles, Global Administrator elevation, system-assigned and user-assigned managed identities |
| 13 | [Azure Key Vault: Creating a Vault, RBAC Roles, and Secrets](2d-azure-resource-access/lab-13-azure-key-vault/) | Key vault creation, soft delete, purge protection, RBAC vs access policies, networking, built-in Key Vault roles, secrets, expiration dates, Bastion with Key Vault |

## Plan and implement workload identities

| # | Lab | Topics |
|---|---|---|
| 14 | [Microsoft Defender for Cloud Apps: Cloud Discovery, App Risk, and Policies](3-workload-identities/lab-14-defender-for-cloud-apps/) | CASB, shadow IT, connectors, automatic log upload, log collectors, snapshot reports, custom log parser, app risk scores, sanctioned vs unsanctioned apps, user and IP investigation, policy templates |
| 15 | [App Registration in Microsoft Entra ID](3-workload-identities/lab-15-app-registration/) | App admin roles, application proxy, application objects vs service principals, multitenant consent flow, registering an app, credentials, optional claims, delegated vs application permissions, admin consent, app roles, manifest, owners |
| 16 | [Enterprise Apps in Microsoft Entra ID](3-workload-identities/lab-16-enterprise-apps/) | Application ID vs object ID, sign-in/assignment/visibility settings, user assignment with app roles, user and admin consent, permission classifications, application proxy and private network connector, App Gallery, SSO and provisioning, app collections |
| 17 | [Entitlement Management in Microsoft Entra ID](lab-17-entitlement-management/) | Identity lifecycle, catalogs, access packages, resource roles, request policies, approvals, requestor questions, expiration, access reviews, My Access requests, separation of duties, connected organizations, lifecycle of external users |

**Planned focus areas (SC-300 domains):**
- Implement and manage user identities (users, groups, external identities, hybrid identity)
- Implement authentication and access management (MFA, Conditional Access, Identity Protection)
- Plan and implement workload identities (app registrations, managed identities, enterprise apps)
- Plan and automate identity governance (entitlement management, access reviews, PIM)

[← Back to IAM Labs](../)
