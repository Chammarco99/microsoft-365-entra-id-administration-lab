# Microsoft 365 & Microsoft Entra ID Administration Lab

## Overview

This project demonstrates the deployment and administration of a simulated Microsoft 365 business environment for **MarcoTech LTD**.

The lab was designed to provide hands-on experience with Microsoft 365 administration, Microsoft Entra ID identity and access management, Role-Based Access Control (RBAC), Multi-Factor Authentication (MFA), Conditional Access, Exchange Online, identity troubleshooting, and user lifecycle management.

Rather than only configuring individual Microsoft 365 features, the project follows realistic IT administration scenarios including employee onboarding, departmental access management, least-privilege administration, identity security, shared mailbox administration, sign-in troubleshooting, and employee offboarding.

## Lab Objectives

The objectives of this project were to:

- Create and manage users in Microsoft Entra ID.
- Assign Microsoft 365 licences and services.
- Organise users using departmental security groups.
- Implement Role-Based Access Control (RBAC).
- Apply the Principle of Least Privilege.
- Configure Multi-Factor Authentication (MFA).
- Implement and test a Conditional Access policy.
- Configure and delegate access to an Exchange Online shared mailbox.
- Verify email delivery using Exchange Online Message Trace.
- Investigate authentication failures using Entra ID sign-in logs.
- Perform a simulated employee offboarding process.
- Validate security controls through practical testing.

## Technologies Used

| Technology | Purpose |
|---|---|
| Microsoft 365 Business Premium | Microsoft 365 lab environment and licensing |
| Microsoft Entra ID | Identity and access management |
| Conditional Access | Policy-based access control |
| Microsoft Authenticator | Multi-factor authentication |
| Exchange Online | Email and mailbox administration |
| Exchange Admin Center | Shared mailbox, delegation and mail-flow administration |
| Microsoft 365 Admin Center | User and licence administration |
| Entra Sign-in Logs | Authentication monitoring and troubleshooting |
| Exchange Message Trace | Email delivery verification and troubleshooting |

## Architecture

The lab environment was built around a Microsoft 365 tenant representing **MarcoTech LTD**.

![Microsoft 365 and Entra ID Lab Architecture](diagrams/microsoft-365-entra-architecture.png)

The environment separates identity and access management from productivity services. Microsoft Entra ID provides identity, authentication, group management, RBAC, MFA and Conditional Access controls, while Exchange Online provides mailbox and email services.

## Test Users

| User | Department / Function | Access |
|---|---|---|
| Alice Johnson | Finance | Standard user / Finance security group |
| Bob Smith | Human Resources | Standard user / HR security group |
| Charlie Brown | IT Support | IT security group / Helpdesk Administrator |
| Emergency Access Admin | Emergency administration | Global Administrator |

Charlie was deliberately assigned the **Helpdesk Administrator** role instead of Global Administrator to demonstrate the **Principle of Least Privilege**.

## Implementation

### 1. User and Licence Management

I started by creating user accounts in Microsoft Entra ID to represent employees working in different departments at MarcoTech LTD.

The test users included:

- **Alice Johnson** — Finance
- **Bob Smith** — Human Resources
- **Charlie Brown** — IT Support

I configured the user accounts with appropriate profile information and assigned Microsoft 365 Business Premium licences where required. This helped me understand the relationship between an Entra ID identity and the Microsoft 365 services provided through licensing.

![Created users](screenshots/02-user-management/01-entra-all-users.jpg)

![Microsoft 365 licence assignment](screenshots/02-user-management/03-alice-business-premium-license.jpg)

---

### 2. Security Groups and Access Management

I created departmental security groups to organise users and manage access based on their job function.

The groups used in the lab were:

- `SG-Finance-Users`
- `SG-HR-Users`
- `SG-IT-Users`

For example, Alice was added to `SG-Finance-Users` because she was acting as the Finance user in the lab.

Using security groups provides a more manageable approach to access control than assigning permissions individually to every employee.

![Finance security group membership](screenshots/03-groups-access/01-finance-security-group-membership.jpg)

---

### 3. Role-Based Access Control (RBAC)

I used Microsoft Entra ID roles to practise the Principle of Least Privilege.

Charlie was the IT Support Technician in the lab. Instead of assigning him the highly privileged Global Administrator role, I assigned him the **Helpdesk Administrator** role.

This gave the support account administrative capabilities relevant to its job function without providing unrestricted control of the Microsoft 365 environment.

![Helpdesk Administrator role](screenshots/04-rbac/01-charlie-helpdesk-administrator.jpg)

I also created an emergency access administrator account with the Global Administrator role to explore the concept of maintaining emergency administrative access.

> **Security note:** In a production environment, emergency access accounts require additional planning, monitoring and protection. The account in this project was created only as part of the lab exercise.

### 4. Multi-Factor Authentication and Conditional Access

I configured Multi-Factor Authentication (MFA) using Microsoft Entra Conditional Access to strengthen authentication for standard users.

I created the following Conditional Access policy:

**Policy:** `CA001 - Require MFA for Standard Users`

The policy targeted the standard lab users and required MFA when accessing Microsoft 365 resources.

Before enforcing the policy, I configured it in **Report-only** mode. This allowed me to observe how the policy would affect user sign-ins before enabling it.

During testing, the Conditional Access result showed that additional user action was required because the user had not yet satisfied the MFA requirement.

![Conditional Access policy](screenshots/05-mfa-conditional-access/01-conditional-access-policy.jpg)

---

#### MFA Registration

I registered Microsoft Authenticator as an authentication method for the test user.

This provided a second authentication factor in addition to the user's password.

![MFA authentication method](screenshots/05-mfa-conditional-access/02-mfa-authentication-method.jpg)

---

#### Conditional Access Testing

After confirming the policy configuration and MFA registration, I enabled the Conditional Access policy and performed another user sign-in test.

I then reviewed the Microsoft Entra sign-in logs to verify that the authentication requirement had been satisfied.

The successful sign-in showed that Multi-Factor Authentication was required and that the MFA requirement had been successfully met.

![Successful MFA sign-in](screenshots/05-mfa-conditional-access/03-conditional-access-signin-result.jpg)

This exercise helped me understand the difference between simply enabling MFA and using Conditional Access to control when additional authentication requirements are applied.

It also demonstrated the importance of testing Conditional Access policies before enforcement to reduce the risk of accidentally locking users or administrators out of an environment.

### 5. Exchange Online Administration

I used the Exchange Admin Center to practise mailbox administration and email access management.

#### IT Support Shared Mailbox

I created an **IT Support** shared mailbox to simulate a central support address that employees could use instead of contacting an individual IT technician.

The shared mailbox used the address:

`support@<tenant>.onmicrosoft.com`

![IT Support shared mailbox](screenshots/06-exchange-online/01-it-support-shared-mailbox.jpg)

---

#### Mailbox Delegation

Charlie Brown was acting as the IT Support Technician, so I delegated access to the IT Support shared mailbox.

I configured:

- **Full Access / Read and manage** — allowing Charlie to open and manage the shared mailbox.
- **Send As** — allowing Charlie to send messages that appear to come directly from the IT Support mailbox.

Access was limited to the IT support user rather than being provided to unrelated employees.

![Shared mailbox delegation](screenshots/06-exchange-online/02-shared-mailbox-delegation.jpg)

---

#### Send As Testing

After configuring the permissions, I signed in as Charlie and accessed the shared mailbox.

I then sent a test email from the IT Support address to Alice Johnson.

The message was successfully received with **IT Support** shown as the sender, confirming that the Send As delegation was working correctly.

![Send As email test](screenshots/06-exchange-online/03-send-as-email-test.jpg)

---

#### Exchange Message Trace

I used **Exchange Online Message Trace** to verify the delivery of the test email.

The trace allowed me to check the sender, recipient, timestamp and delivery status. The test message showed a **Delivered** status, confirming that Exchange Online had successfully processed and delivered the message.

![Exchange Message Trace](screenshots/06-exchange-online/04-message-trace-delivered.jpg)

This exercise gave me practical experience with shared mailbox administration, mailbox delegation, Send As permissions and basic Exchange Online mail-flow troubleshooting.

### 6. Identity and Sign-in Troubleshooting

To practise identity troubleshooting, I simulated a scenario where Bob Smith from HR was unable to sign in to Microsoft 365.

Rather than immediately resetting the account, I used **Microsoft Entra sign-in logs** to investigate the authentication failure.

#### Investigating the Failed Sign-in

I located Bob's failed interactive sign-in event and reviewed the authentication details.

The sign-in log showed:

- **Status:** Failure
- **Error code:** `50126`
- **Failure reason:** Invalid username or password

This indicated that the authentication problem was related to the user's credentials rather than the Conditional Access policy.

![Failed sign-in investigation](screenshots/07-troubleshooting/01-bob-failed-signin-invalid-credentials.jpg)

---

#### Remediation and Verification

After identifying the cause, I performed an administrator password reset and tested the account again using the new credentials.

Because Bob was included in the Conditional Access policy, MFA requirements also applied during the authentication process.

I then returned to the Entra sign-in logs and verified that the new authentication attempt completed successfully.

![Successful MFA sign-in](screenshots/07-troubleshooting/02-bob-successful-mfa-signin.jpg)

The troubleshooting process followed this workflow:

**User reports issue → Review sign-in logs → Identify failure reason → Remediate the account → Test authentication → Verify successful sign-in**

This exercise helped me understand why sign-in logs are important when troubleshooting Microsoft 365 authentication problems. Instead of assuming the cause, I used the available log information and error code to identify the issue before applying a fix.

### 7. User Offboarding and Access Revocation

To practise the employee leaver process, I simulated the offboarding of Alice Johnson from the Finance department.

The objective was to ensure that the user could no longer access company resources and that access and licensing assigned during employment were removed.

#### Blocking User Sign-in

I first blocked Alice from signing in to Microsoft 365.

This prevents new authentication attempts while keeping the account available for administrative tasks that may still be required during the offboarding process.

![Alice sign-in blocked](screenshots/08-user-offboarding/01-alice-signin-blocked.jpg)

---

#### Revoking Sessions and Removing Access

I revoked the user's existing sign-in sessions so that previously authenticated sessions would be required to authenticate again.

I also removed Alice from the Finance security group, removing the group-based access associated with her Finance role.

![Finance access removed](screenshots/08-user-offboarding/02-alice-finance-access-removed.jpg)

---

#### Licence Removal

After removing access, I removed the Microsoft 365 Business Premium licence assigned to Alice.

This simulated reclaiming a licence that could later be assigned to another employee.

![Microsoft 365 licence removed](screenshots/08-user-offboarding/03-alice-license-removed.jpg)

---

#### Offboarding Verification

Finally, I attempted to authenticate using Alice's account after sign-in had been blocked.

The authentication attempt failed, and I reviewed the event in the Microsoft Entra sign-in logs to verify that access had been denied.

![Blocked sign-in verification](screenshots/08-user-offboarding/04-alice-blocked-signin-verification.jpg)

The offboarding workflow used in the lab was:

**Block sign-in → Revoke sessions → Remove group access → Remove licence → Test access → Verify denial**

This exercise demonstrated the importance of removing both authentication and authorization when an employee leaves an organisation.

> **Production consideration:** A real offboarding process may also require mailbox and OneDrive data preservation, ownership transfer, retention policies, device management, legal requirements, application access removal and other organisation-specific controls. This lab focused primarily on Microsoft 365 identity and access administration.

## Security Lessons Learned

Building this lab helped me understand that Microsoft 365 administration is not only about creating users and assigning licences. Identity security and access control are a major part of administering a cloud environment.

Some of the main lessons I took from the project were:

- **Least privilege:** Administrative users should receive only the permissions required for their responsibilities. This was demonstrated by assigning Charlie the Helpdesk Administrator role rather than Global Administrator.
- **MFA:** Passwords alone should not be relied upon to protect user accounts. MFA provides an additional layer of authentication.
- **Conditional Access:** Access policies can be used to enforce security requirements based on defined conditions. Testing policies in Report-only mode before enforcement can help identify potential problems.
- **Group-based access:** Security groups provide a more scalable way to organise users and manage access than assigning permissions individually.
- **Logging and monitoring:** Entra sign-in logs and Exchange Message Trace provide valuable evidence when investigating authentication and email-delivery issues.
- **User lifecycle management:** Access needs to be managed throughout the lifecycle of an account, from initial provisioning through to offboarding.
- **Verification:** A configuration should be tested after implementation rather than assuming it works as expected.

---

## Skills Demonstrated

Through this project I gained hands-on experience with:

- Microsoft 365 administration
- Microsoft Entra ID
- Identity and Access Management (IAM)
- User provisioning and deprovisioning
- Microsoft 365 licence management
- Security group administration
- Role-Based Access Control (RBAC)
- Principle of Least Privilege
- Multi-Factor Authentication (MFA)
- Conditional Access
- Microsoft Authenticator
- Exchange Online administration
- Shared mailbox management
- Full Access and Send As delegation
- Exchange Message Trace
- Entra ID sign-in logs
- Authentication troubleshooting
- User offboarding and access revocation

---

## Project Outcome

By completing this lab, I gained practical experience administering a Microsoft 365 environment rather than relying only on theoretical knowledge.

I worked through the lifecycle of cloud identities by creating users, assigning licences and group memberships, applying administrative roles, enforcing MFA through Conditional Access, administering Exchange Online, troubleshooting authentication failures, and finally removing access during an employee offboarding scenario.

One of the most useful parts of the project was learning to verify configurations using sign-in logs, authentication results and message tracing instead of assuming that a configuration had worked.

This lab also helped me understand how Microsoft Entra ID and Microsoft 365 work together: Entra ID manages identities, authentication and access, while Microsoft 365 services such as Exchange Online provide the resources those identities access.

---

## Future Improvements

If I extend this lab in the future, I would like to explore:

- Microsoft Intune device management
- Entra ID Privileged Identity Management (PIM)
- Additional Conditional Access scenarios
- Microsoft Defender for Office 365
- Microsoft Defender for Endpoint
- Self-Service Password Reset (SSPR)
- Dynamic group membership
- Access Reviews
- Hybrid identity with Windows Server Active Directory
- PowerShell and Microsoft Graph automation

---

## Disclaimer

This project was completed in a personal lab environment using fictional users and a fictional organisation. It was created for educational and portfolio purposes and does not represent a production deployment.
