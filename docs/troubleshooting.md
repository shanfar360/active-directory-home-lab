
# Virtualized Home Lab – Troubleshooting & Stability Notes

## Overview

This document highlights a real-world virtualization issue encountered during the setup of my Windows-based Active Directory home lab on **Windows 11 using VirtualBox** and explains how it was diagnosed and resolved. This reflects practical troubleshooting skills commonly required in enterprise IT environments.

---

## Environment

* **Host OS:** Windows 11
* **Hypervisor:** Oracle VirtualBox 7.1
* **CPU:** Intel (VT-x enabled)
* **Storage:** External SSD
* **Guest OS:**

  * Windows Server (Active Directory, DNS, DHCP)
  * Ubuntu Linux (utility / testing VM)

---

## Problem Encountered

When starting the **Windows Server VM**, VirtualBox crashed with the error:

> **VirtualBoxVM.exe – The instruction at referenced memory could not be written**

Key observations:

* Ubuntu VM worked without issues
* VirtualBox installed correctly
* Hardware virtualization was enabled

This indicated the problem was **specific to the Windows guest configuration**, not the host system or storage.

---

## Root Cause Analysis

The issue was caused by a combination of:

1. **Legacy chipset (PIIX3)** used for a modern Windows guest
2. **Windows 11 virtualization security features** (Hyper-V / VBS conflicts)
3. **Graphics controller incompatibility** with VirtualBox 7.x

Although Hyper-V features were unchecked, Windows 11 can still load virtualization-based security components that interfere with VirtualBox.

---

## Resolution Steps

### 1. Windows Host Configuration

* Disabled the following Windows features:

  * Hyper-V
  * Virtual Machine Platform
  * Windows Hypervisor Platform
  * Windows Subsystem for Linux (WSL)

* Disabled **Memory Integrity (VBS)**:

  * Windows Security → Device Security → Core Isolation → Memory Integrity = OFF

* Verified hypervisor was disabled:

  ```bat
  systeminfo | findstr /i hypervisor
  ```

---

### 2. VirtualBox VM Configuration (Critical Fix)

#### System → Motherboard

* **Chipset:** Changed from **PIIX3 → ICH9** ✅
* **I/O APIC:** Enabled
* **EFI:** Disabled (legacy Windows install)

#### System → Processor

* CPUs: 2
* PAE/NX: Enabled

#### Display

* Graphics Controller: **VMSVGA**
* Video Memory: 128 MB
* 3D Acceleration: Disabled

#### Saved State

* Discarded previous saved state before restarting the VM

---

## Result

* Windows Server VM started successfully
* Stable operation with Active Directory, DNS, and DHCP roles
* Ubuntu VM continued to function normally
* No further VirtualBox crashes or memory errors

---

## Key Takeaways

* Modern Windows guests should use **ICH9**, not legacy PIIX3
* Windows 11 security features can silently interfere with third-party hypervisors
* Linux guests may work even when Windows guests fail
* Proper chipset and graphics configuration is critical in VirtualBox 7.x

---

## Why This Matters

This issue and resolution demonstrate:

* Real-world virtualization troubleshooting
* Understanding of Type-1 vs Type-2 hypervisors
* Awareness of Windows 11 security architecture
* Practical experience configuring enterprise-style lab environments

This mirrors the kind of problems encountered in production IT environments and highlights strong diagnostic and problem-solving skills.

---


