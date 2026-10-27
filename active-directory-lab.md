**Tags:** #cybersecurity #homelab #activedirectory #helpdesk
**Status:** In Progress...
**Date Started:** 2026-10-19

# Objective: 
To build a functional Active Directory (AD) environment from scratch and practice common Tier 1 Help Desk tasks, including user provisioning, password resets, account unlocks, and Group Policy enforcement.

# Environment Specs:
- **Hypervisor:** VirtualBox
- **Domain Controller (DC01):** Windows Server  2022 Standard (Desktop Experience)
- **Domain Name:** ~~homelab.local~~ --> corp.local
- **Client (Client1):** Windows 11 Pro

# Task Checklist
Phase 1: Foundation & Setup:
- [x] Install Windows Server 2022 (Desktop Experience)
- [x] Rename the computer to `DC01`
- [x] Install the **Active Directory Domain Services (AD DS)** role
- [x] Promote the server to a Domain Controller
- [x]  Create a new forest called: `corp.local`

Phase 2: Mock Company Setup
- [x] Open **Active Directory Users and Computers (ADUC)**.
- [x] Create Organizational Units (OUs):
    - [x] `Company_Name`
    - [x] `Departments` (Sub-OUs: `IT`, `HR`, `Sales`)
    - [x] `Workstations`
    - [x] `Servers`
- [x] Create Test Users:
    - [x] `j_doe` (Sales)
	    - John Doe (JD): j_doe@homelab.local
	    - Password: ~~Deejay12345~~ --> Wasd12345
    - [x] `jane_d` (HR)
	    - Jane Doe (JD): jane_d@homelab.local
	    - Password: ~~Lovelything12~~ --> Thinglovely12
    - [x] `jaycee` (IT)
	    -  Jayce Park (JP): jaycee@homelab.local
		- Pass: ~~Peejays123~~ --> Jayspee123
- [x] Create Security Groups:
    - [x] `IT_Admins` (Add `admin1` to this group)
  
Image provided below:
<img width="1022" height="852" alt="Organizational_units_(Departments)" src="https://github.com/user-attachments/assets/6e21fa5f-9420-40a0-b851-b703e71e4826" />


Phase 3: Help Desk Ticket Simulations
- [x] **Ticket 1: Password Reset**
    - [x] Right-click `jdoe` → Reset Password.
    - [x] Check "Require user to change password at next logon".
    - [x] <img width="1021" height="777" alt="Password_Reset" src="https://github.com/user-attachments/assets/184a01f8-7864-43a8-ba7f-643f5ff0ffd7" />

- [x] **Ticket 2: Account Unlock**
    - [x] Trigger a lockout (enter wrong password 5 times).
    - [x] Locate locked user in ADUC (red padlock icon).
    - [x] Right-click → Unlock Account.
    - [x] <img width="1011" height="753" alt="Lockout" src="https://github.com/user-attachments/assets/05c77c43-bec4-422c-beb3-56695cdcee0d" />
    <img width="1022" height="769" alt="Unlocking" src="https://github.com/user-attachments/assets/b542dd0d-703e-4e84-9f90-89e96b7f472c" />
    <img width="1000" height="771" alt="Unlock_success" src="https://github.com/user-attachments/assets/c4326e2f-fe31-4a08-91bc-779209f42af0" />
    
- [ ] **Ticket 3: New Hire Onboarding**
    - [ ] Create a new user in the `HR` OU.
    - [ ] Add them to the `HR_Staff` security group.
    - [ ] 

Phase 4: Group Policy (Security)
- [ ] Open **Group Policy Management**.
- [ ] Create GPO: `Password_Policy` (Linked to Domain).
    - [ ] Enable "Password must meet complexity requirements".
- [ ] Create GPO: `Sales_Screensaver` (Linked to `Sales` OU).
    - [ ] Set screen lock timeout to 10 minutes.
- [ ] *[Insert Screenshot Here]*

--- 
**Troubleshooting Notes**
- **Issue:** The DNS Server service was stopped after installation.
  **Fix:** Opened `services.msc`, manually started the "DNS Server" service, and set it to Automatic. Verified network connectivity.

- **Issue:** Trying to log in to the Domain Controller with a standard user (jane_d) resulted in an error
  **Fix:** Edited the "Default Domain Controller Policy" GP. Navigated to `Default Domain Policy > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > User Rights Assignment` and added `Domain Users` to the "Allow log on locally" policy. Ran `gpudate /force` to apply.

- **Issue:** Entering wrong password five times does not lock the account.
  **Fix:** in `Default Domain Policy > Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`, set threshold to be `5`, then run `gpupdate /force`.



---
**What I Learned**
- How to create and navigate through a virtual machine.
- How to create a virtual server and client and how to connect them.
- How AD organizes users through OUs and Groups.
- The difference between a password reset and an account unlock.
- How Group Policy applies to specific OUs rather than the whole domain.
