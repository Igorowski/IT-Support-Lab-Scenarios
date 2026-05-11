
# Password Reset (Active Directory)

## Overview

This scenario demonstrates the password reset process for an Active Directory user who is unable to log in due to a forgotten password. The workflow follows a standard helpdesk procedure within a Windows Server 2019 domain environment.

---

## Environment

* Domain Controller: Windows Server 2019
* Client Machine: Windows 10
* Active Directory Domain: `igrlab.local`
* DHCP Server hosted on Domain Controller
* DNS hosted on Domain Controller
* Virtualization: Oracle VirtualBox

---

## Initial Working State (Baseline)

The user account `john.johnson` was verified as active and functional prior to the issue. Login was confirmed using the `whoami` command after successful authentication.

The account was protected with a known password (`Password1`) used only for lab validation purposes.

<img width="221" height="87" alt="image" src="https://github.com/user-attachments/assets/ace1ee0a-f53d-44ac-8145-2976fc958ecd" />

---

## Issue Simulation

### Reported Problem

The user reported being unable to log in after forgetting the password. Authentication attempts failed at the Windows logon screen.

<img width="352" height="196" alt="image" src="https://github.com/user-attachments/assets/6743e0e9-ac2a-4af5-a5eb-556b5da4eeb0" />

---

## Troubleshooting Process

### Step 1 — Password Reset in Active Directory

On the Domain Controller:

Active Directory Users and Computers (ADUC) was used to perform the reset:

```
ADUC → User Account → Reset Password
```

A new temporary password was assigned:

```
Temporary1
```

The option **User must change password at next logon** was enabled to enforce secure credential update on first login.

Note: If **Password never expires** is enabled on the account, it should be reviewed and disabled depending on domain policy, as it may conflict with password rotation policies.

<img width="361" height="154" alt="image" src="https://github.com/user-attachments/assets/202a914e-e20e-4614-90f2-f846af900792" />

---

### Step 2 — First Login with Temporary Password

The user successfully authenticated using the temporary password.

Immediately after login, Windows enforced a password change requirement as configured in ADUC.

<img width="592" height="250" alt="image" src="https://github.com/user-attachments/assets/c1cd9606-8636-410f-b3f6-404fd9627b9f" />

---

### Step 3 — Password Update

The user was prompted to set a new password that complies with domain password policy requirements. After validation, the password change was completed successfully.

<img width="371" height="226" alt="image" src="https://github.com/user-attachments/assets/add1dcec-f9be-4d39-ab64-78aca0170f02" />

---

## Outcome

The user regained access to the account after resetting credentials and completing the forced password update process.

---

## Key Learnings

* Active Directory password reset procedure using ADUC
* Enforcement of password change at next logon
* Behavior of temporary credentials in Windows authentication flow
* Interaction between account flags such as password policies and expiration settings
* Standard helpdesk workflow for account recovery scenarios

---

## Skills Demonstrated

* Active Directory administration
* Windows Server 2019 management
* User account troubleshooting
* Identity and access management (IAM) basics
* Helpdesk incident resolution workflow
