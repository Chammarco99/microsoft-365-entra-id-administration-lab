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
