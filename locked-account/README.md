# Locked Account

## Overview
This scenario demonstrates how an Active Directory account can become locked after multiple failed login attempts.

The objective was to simulate a common helpdesk situation where a user is unable to log into a workstation because the account has been locked by the domain security policy.

The process of identifying and unlocking the account is also demonstrated.

---

# Environment

- Domain Controller: Windows Server 2019
- Client Machine: Windows 10
- Active Directory Domain: `igrlab.local`
- DHCP Server hosted on Domain Controller
- DNS hosted on Domain Controller
- Oracle VirtualBox lab environment

---

# Environment Setup

The Account Lockout Policy was configured in the Default Domain Policy to help protect domain accounts against unauthorized access attempts and brute-force attacks.

```text
Group Policy Management
→ Default Domain Policy
→ Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Account Lockout Policy
````

The lockout threshold was configured to:

```text
3 invalid logon attempts
```

<img width="415" height="507" alt="image" src="https://github.com/user-attachments/assets/65c5b62b-9ca6-40c7-b802-3e8136b64023" />

---

# Initial Working State (Baseline)

The domain account was verified to be operational before testing the security policy.

<img width="601" height="510" alt="image" src="https://github.com/user-attachments/assets/68e5d51a-0da0-4a1a-9a3a-0b5863e93518" />

---

# Issue Simulation

## Change Introduced

An incorrect password was entered three consecutive times during login attempts.

---

# Symptoms Observed

After the third failed attempt, Windows displayed the following message:

```text
The referenced account is currently locked out and may not be logged on to.
```

<img width="686" height="436" alt="image" src="https://github.com/user-attachments/assets/225b75cf-9d2e-40ed-857e-aba945c5f85e" />

---

# Troubleshooting Process

## Step 1 — Verify Account Status

A login attempt using the correct password was performed to confirm that the issue was not caused by incorrect credentials.

The account remained inaccessible.

<img width="922" height="534" alt="image" src="https://github.com/user-attachments/assets/534b8992-6d76-4846-aaba-dcb3acd289f8" />

---

## Step 2 — Inspect Account Properties

On the Domain Controller:

```text
Active Directory Users and Computers
→ User Properties
→ Account
```

The account displayed the option to unlock the user.

<img width="409" height="531" alt="image" src="https://github.com/user-attachments/assets/74079b23-5ac5-46de-b6c0-9ffb5a213a29" />

---

## Step 3 — Unlock the Account

The account was manually unlocked in Active Directory Users and Computers.

Changes were applied successfully.

---

# Root Cause

The domain security policy locked the account after three consecutive failed authentication attempts.

---

# Verification

After unlocking the account, the user was able to log in successfully before the lockout duration expired.

<img width="632" height="473" alt="image" src="https://github.com/user-attachments/assets/c19f5a7f-a251-4299-9b9d-1c84f5392310" />

---

# Key Learnings

* Understanding Active Directory account lockout policies
* Understanding failed authentication behavior
* Troubleshooting domain login issues
* Unlocking user accounts in Active Directory
* Understanding account security policies

---

# Skills Demonstrated

* Active Directory administration
* Helpdesk troubleshooting
* User account management
* Group Policy configuration
* Windows authentication troubleshooting
* Domain environment administration

