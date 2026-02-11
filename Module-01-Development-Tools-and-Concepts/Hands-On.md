# 🛠️ Hands-On: WSL & Ubuntu Environment Setup
**Chapter 1 | Week 1 | Session 1**

This document tracks the practical installation of the **Windows Subsystem for Linux (WSL)**, the configuration of **Ubuntu 24.04**, and the verification of the L1 Hypervisor architecture.

---

## 🐧 Core Concepts: WSL Architecture

Before installation, it is important to understand how WSL 2 differs from traditional virtualization (like VirtualBox or VMware).

### **L1 Hypervisor vs. Type 2**
WSL 2 utilizes a **Type 1 (L1) Hypervisor**. Instead of running as an application on top of Windows, it runs at the same privilege level as the Windows OS.

* **Direct Hardware Access:** It connects directly to the **CPU**, offering near-native performance.
* **Linux Kernel:** It includes a real Linux kernel maintained by Microsoft, ensuring full compatibility with Docker and Data Science tools.

[Image of Type 1 vs Type 2 hypervisor architecture]

---

## 🐧 Part 1: Ubuntu Distribution Setup
### **1. Enable Windows Features**

Before the OS can boot, the following features must be active in "Turn Windows features on or off":

    - [x] Virtual Machine Platform

    - [x] Windows Hypervisor Platform

    - [x] Windows Subsystem for Linux

### **2. Install Ubuntu 24.04**

I listed the available distributions and selected Ubuntu 24.04 (LTS) for its stability in data science workflows.
```wsl --list --online```

```wsl --install ubuntu-24.04```

### **3. First Boot & User Setup**

Launched the Ubuntu environment:
```wsl```

    [!IMPORTANT]
    During this step, I created a Unix Username and Password.
    Note: The password characters remain invisible while typing.

### **🔄 Part 2: System Optimization & Updates**

Immediately after launching Ubuntu, I performed a full system update to ensure all libraries were current.

- Update package repositories 
```sudo apt update```
- Upgrade all installed packages
```sudo apt upgrade -y```

---
### **Accessing Ubuntu via PowerShell**

Once the WSL engine is running, you can launch your environment at any time by calling the distribution name:

Syntax: wsl -d <DistributionName>
```wsl -d Ubuntu-24.04```

---
### **Final Environment Status**



| **Objective** | **Status** |
| :--- | :--- |
| **WSL Engine** | Installed (Version 2.6.3+) |
| **Architecture** | Verified L1 Hypervisor (WSL 2) |
| **Distribution** | Ubuntu 24.04 LTS Configured |
| **Environment** | **Ready for Development** |

---

**Conclusion:** The environment is successfully bridged.

---