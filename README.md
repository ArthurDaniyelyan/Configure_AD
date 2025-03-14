<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

# On-Premises Active Directory in Azure

## Overview
This project demonstrates the setup of an On-Premises Active Directory (AD) environment deployed in Microsoft Azure. The goal is to showcase cloud networking, identity management, and Windows administration skills.

## 1️ Azure Environment Setup
###  Create a Virtual Network (VNet)
1. Log in to Azure Portal.
2. Navigate to Virtual Networks → Click Create.
3. Configure:
   - Resource Group
   - Region
   - VNet Name: `OnPrem-AD-VNet`
   - Address Space: `10.0.0.0/16`
4. Create Subnets:
   - AD-Subnet: `10.0.1.0/24`
   - Client-Subnet: `10.0.2.0/24`
5. Click Review + Create → Create.

## 2️ Deploy the Active Directory Domain Controller**
###  Create a Windows Server VM
1. Go to Virtual Machines → Create a VM.
2. Choose:
   - Image: Windows Server 2022 Datacenter
   - VM Size: Standard B2ms (2 vCPUs, 8 GB RAM)
   - Subnet: `AD-Subnet`
   - Public IP: Disabled (for security)
3. Click Next: Networking → Review + Create → Create.

### Configure Active Directory Domain Services (AD DS)
1. Connect to the VM via RDP.
2. Open Server Manager → Add Roles and Features.
3. Install Active Directory Domain Services and DNS Server.
4. Click Promote this server to a domain controller.
5. Select Add a New Forest → Enter a Domain Name (e.g., `mycompany.local`).
6. Set a Directory Services Restore Mode (DSRM) password**.
7. Click Next → Install → Reboot.

## 3️ Setup Client VM & Join Domain
### Create a Windows 10/11 Client VM
1. Create another Windows 10/11 VM.
2. Assign it to the Client-Subnet.
3. Change its DNS settings to point to the Domain Controller’s Private IP.

### Join the Client to the Domain
1. Connect to the Client VM via RDP.
2. Open System Properties → Change Settings.
3. Under Computer Name, click Change.
4. Select Domain and enter `mycompany.local`.
5. Enter Administrator Credentials from the AD VM.
6. Restart the VM.

## 4️ Configure Group Policies (GPO)
1. On the DC, open Group Policy Management.
2. Create a new GPO under `mycompany.local`.
3. Apply settings like Password Policies, Software Restrictions, or Drive Mappings.
4. Link the GPO to an Organizational Unit (OU).

## 5 Test Authentication
 Log in to the Client VM using a Domain User Account.  
 Run `gpupdate /force` to apply policies.  
 Use `ping DC-name` to verify connectivity.  

## Key Skills Demonstrated
- Azure Virtual Networking 
- Windows Server & Active Directory 
- Domain Joining & GPO Management  
- Basic Cybersecurity & IAM Concepts  

<h2>Deployment and Configuration Steps</h2>
