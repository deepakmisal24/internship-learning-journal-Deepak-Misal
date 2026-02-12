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

# 🛠️ Hands-On: Git Setup & GitHub Deployment
**Chapter 1 | Week 1 | Session 2**

This guide documents the practical steps taken to install Git within the WSL environment and the workflow used to push local projects to a remote GitHub repository.

---

## 🏗️ Part 1: Installing Git in the Local System (WSL)

Since development for this course happens in the Linux subsystem, Git must be installed directly within the Ubuntu environment to interface correctly with the project files.

### **1. Install Git inside Ubuntu (WSL)**
Open your Ubuntu terminal and execute the following commands to ensure the package manager is current and Git is installed:

```bash
# Update your package list
sudo apt update

# Install Git
sudo apt install git -y

# Verify the installation
git --version
```

### **2. Configure your Git Identity**
Git requires a registered identity to label "save-points" (commits). This information is attached to every change you make.

```bash
# Set global configuration
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### **3. Initialize Git in your Project**
Once the environment is configured, initialize the tracking engine within your specific project folder:

1. Open your project folder in **VS Code** (`File > Open Folder`).
2. Open the **Integrated Terminal** .
3. Run the initialization command:

```bash
# Creates the hidden .git directory to start tracking your files
git init
```

---
## 🚀 Part 2: Pushing to GitHub
After initializing the local repository, follow these steps to upload your code to the cloud.

### **1. Prepare Your Local Files**
Record your changes officially in the local repository history.



```bash
# 1. Initialize Git (only required once per project)
git init

# 2. Stage your files (move them to the "Staging Area")
git add .

# 3. Commit your changes (create a permanent snapshot)
git commit -m "Your descriptive message here"
```
### **2. Create the Bridge to GitHub**
To connect your local repository to a remote server, you must link it to a specific GitHub URL and name that link **"origin"**.

1. Create a new repository on **GitHub**.
2. Copy the URL (e.g., `https://github.com/username/repo.git`).
3. Run the following in your terminal:



```bash
# Link the local folder to the remote URL example
git remote add origin [https://github.com/deepakmisal24/internship-learning-journal-Deepak-Misal.git](https://github.com/deepakmisal24/internship-learning-journal-Deepak-Misal.git)
```

### **3. The Final Push**
Upload your local commits to the remote "origin" server on the "main" branch.



```bash
# Use the -u flag the first time to track the remote branch
git push -u origin main
```

### **Key Terms**

* **Origin:** The conventional nickname for your remote GitHub URL.
* **Main:** The default name of your primary development branch.

---