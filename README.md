# Virtualized Home Lab – Active Directory & Network Services

## Overview
This project demonstrates a fully virtualized Windows Server 2022 home lab designed to simulate a real-world enterprise Active Directory environment. The lab was built using Oracle VirtualBox to gain hands-on experience with identity management, networking, and core Windows Server services.

## Lab Architecture
- **Host Machine**
  - Oracle VirtualBox hypervisor

- **Windows Server 2022 (Domain Controller)**
  - Active Directory Domain Services (AD DS)
  - DNS
  - DHCP
  - Routing and Remote Access (RRAS) with NAT
  - Dual NIC configuration:
    - External (Internet-facing)
    - Internal (Private domain network)

- **Windows Client**
  - Domain-joined workstation
  - Receives IP configuration via DHCP
  - Authenticates using domain credentials
  - Accesses the internet through RRAS/NAT

## Key Configuration Steps
- Deployed virtual machines using Oracle VirtualBox
- Promoted Windows Server 2022 to a Domain Controller
- Configured DNS for domain name resolution
- Created and configured a DHCP scope
- Enabled RRAS and configured NAT for internet access
- Joined a Windows client machine to the domain
- Verified authentication, DNS resolution, and connectivity

## Skills Demonstrated
- Windows Server 2022 administration
- Active Directory (AD DS)
- DNS and DHCP
- Routing and Remote Access (RRAS / NAT)
- Network segmentation and IP addressing
- Virtualization with Oracle VirtualBox
- Troubleshooting domain and network issues

## Diagram

Here’s a visual overview of my Virtualized Home Lab setup:

![Virtualized Home Lab](https://github.com/shanfar360/active-directory-home-lab/blob/6e6ceec6a32f7fd512fd0d1bd2e4e74f164755a2/images/home_lab_diagram.png.png)

This diagram illustrates the full lab architecture, including network layout, servers, and client connections.


## Future Improvements
- Group Policy Objects (GPOs)
- File server and NTFS permissions
- WSUS
- Monitoring and logging
- Cloud or hybrid integration (Azure / AWS)

## Summary
This lab reflects real enterprise infrastructure and demonstrates my ability to design, deploy, and troubleshoot a domain-based Windows Server environment using virtualization.
