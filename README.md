# active-directory-account-lockout-lab

## Objective
Configure an account lockout policy in Active Directory, trigger repeated failed login attempts on a domain-joined Windows client, and investigate the resulting authentication and lockout events on the domain controller.

## Lab Environment
- **Domain Controller:** Windows Server 2025
- **Client System:** Windows client VM
- **Domain:** `terrylab.local`
- **Virtualization Platform:** VirtualBox

## Skills Demonstrated
- Active Directory administration
- Group Policy configuration
- Account lockout policy management
- Domain authentication troubleshooting
- Windows Event Viewer analysis
- Identity security monitoring

## Project Overview
This lab builds on a working Active Directory environment by applying a domain-wide account lockout policy through Group Policy, testing that policy with repeated failed sign-in attempts, and reviewing the resulting lockout events on the domain controller.

## Project Steps

### 1. Configured the domain environment
- Built a Windows Server domain controller
- Configured DNS for Active Directory
- Joined a Windows client to the `terrylab.local` domain
- Created test domain users for authentication testing

### 2. Configured account lockout policy
On the domain controller, I opened **Group Policy Management** and edited the **Default Domain Policy** under:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`

Configured settings:
- **Account lockout threshold:** 5 invalid logon attempts
- **Account lockout duration:** 15 minutes
- **Reset account lockout counter after:** 15 minutes

### 3. Applied Group Policy
Forced Group Policy updates to apply the new policy settings to the lab environment.

### 4. Triggered repeated failed logins
On the domain-joined Windows client, I attempted multiple failed sign-ins using the domain account:

`terrylab\analyst1`

This triggered the configured account lockout threshold.

### 5. Investigated lockout activity
On the domain controller, I reviewed the **Security** log in **Event Viewer** and filtered for relevant events.

Primary event reviewed:
- **4740** — A user account was locked out

The log confirmed that the domain account `TERRYLAB\analyst1` was locked out successfully.

## Event IDs Reviewed
- **4740** — A user account was locked out

## Results
The lab successfully demonstrated:
- Group Policy-based account lockout enforcement
- Domain user lockout after repeated failed sign-in attempts
- Centralized logging of account lockout activity on the domain controller
- Validation of Active Directory identity security controls in a home lab environment

## Screenshots

### Account Lockout Policy
![Account Lockout Policy](https://github.com/Tl39455/active-directory-account-lockout-lab/blob/ca27614bc5d15626483920087fe2b6ee1745d47e/account-lockout-policy.png)

![](https://github.com/Tl39455/active-directory-account-lockout-lab/blob/ca27614bc5d15626483920087fe2b6ee1745d47e/account-lockout-policy.png)

![](https://github.com/Tl39455/active-directory-account-lockout-lab/blob/ca27614bc5d15626483920087fe2b6ee1745d47e/account-lockout-policy.png)

### Lockout Event in Event Viewer
![Lockout Events](https://github.com/Tl39455/active-directory-account-lockout-lab/blob/82202ad40176f4bb854d5868254c0ab61e8122b0/group-policy-force-update.png)

![](https://github.com/Tl39455/active-directory-account-lockout-lab/blob/ca27614bc5d15626483920087fe2b6ee1745d47e/account-lockout-policy.png)

## Outcome
Successfully configured and tested an Active Directory account lockout policy in a domain environment, then validated the resulting lockout event on the domain controller through Windows Event Viewer.

## Resume Bullet
- Configured an Active Directory account lockout policy through Group Policy, triggered repeated failed domain logins on a domain-joined Windows client, and validated account lockout events in Windows Event Viewer on the domain controller.
