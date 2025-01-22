# Active-Directory-Lab-using-Oracle-VirtualBox

![AltText](ad.png)

# Overview

![AltText](diagram.png)
In this lab, I set up an Active Directory environment using Oracle VirtualBox, including a domain controller and virtual network. PowerShell scripts were used to automate user creation and management. This project was focused around learning AD configuration, automation, and system administration.

# Requirements
- **Software**:
  - VirtualBox (for virtualization)
  - Windows 10 ISO (for client machine)
  - Windows Server 2019 ISO (for domain controller)
  
- **Network Configuration**:
  - Two Network Interface Cards (NICs) per machine
    - **NIC 1**: Connected to the Internet (DHCP enabled)
    - **NIC 2**: Internal network (static IP configuration)

# Environment Setup

## 1. VirtualBox Setup
![AltText](vm_manager.png)
- Create two virtual machines (VMs) in VirtualBox:
  - One VM is configured as **Server 2019** for the domain controller (DC).
  - One VM is configured as **Windows 10** for the client machine.

## 2. Networking Configuration
![AltText](diagram_nic.png)
- **NIC 1** (for internet connection):
  - Set to obtain an IP address automatically via DHCP from the home router.
- **NIC 2** (for internal network):
  - Static IP configuration:
    - **IP Address**: `172.16.0.1`
    - **Subnet Mask**: `255.255.255.0`
    - **Default Gateway**: Leave blank
    - **DNS**: `127.0.0.1`
  
![AltText](nic_internal.png)
![AltText](nic_config.png)

## 3. Domain Controller Configuration
![AltText](ad_domain_diagram.png)
- Install **Active Directory Domain Services (AD DS)** on Server 2019.
- Configure the domain with the Fully Qualified Domain Name (FQDN): `mydomain.com`.

![AltText](domain.png)

## 4. RAS/NAT (Routing)
![AltText](routing_diagram.png)
- Install the **Remote Access Service (RAS)** role on the domain controller to enable NAT.
- Configure NAT to allow internet access for devices on the internal network:
  1. Open the **Routing and Remote Access** console.
  2. Configure NAT for **NIC 1** (external interface connected to the internet).
  3. Verify that the internal network (connected via **NIC 2**) can access the internet through the NAT configuration.

![AltText](routing.png)

## 5. DHCP
![AltText](dhcp_diagram.png)
- Installed and configured the **DHCP Server** role on the domain controller.
- Set up a DHCP scope to assign IP addresses dynamically to devices on the internal network:
  - **IP Range**: `172.16.0.100 - 172.16.0.200`
  - **Subnet Mask**: `255.255.255.0`
  - **Default Gateway**: `172.16.0.1`
  - **DNS Server**: `172.16.0.1`
- Verified that the Windows 10 client successfully received an IP address and could communicate with the domain controller and access the internet via NAT.
  
![AltText](dhcp.png)

## 6. Add Users via. Powershell script



