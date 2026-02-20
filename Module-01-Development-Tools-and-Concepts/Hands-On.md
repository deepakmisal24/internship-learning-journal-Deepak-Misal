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
---

# 🛠️ Hands-On: UV installation and gemini api setup
**Chapter 1 | Week 1 | Session 3**

This practical session covers the installation of the UV package manager, setting up the LLM CLI tool, and authenticating with Google's Gemini to enable AI capabilities directly within your WSL/Ubuntu environment.

---

## 🏗️ Part 1: UV & LLM Tool Installation

**UV** is an extremely fast Python package installer and resolver, written in Rust, designed to replace `pip`. We use it here to manage our AI command-line tools.



### **1. Install UV**
Open your Ubuntu terminal and install UV using the official standalone script:

```bash
# Install UV via the curl script
curl -LsSf https://astral.sh/uv/install.sh | sh
```
Then close the current terminal and reopen ubuntu terminal
```bash
#To check whether UV has been installed properly
uv --version
```


### **2. Manage the LLM Tool**
Once UV is installed, use it to install the `llm` tool. This tool acts as a universal interface for various AI models.



**Install:**
```bash
uv tool install llm
```

**Uninstall:(If needed)**
```bash
uv tool uninstall llm
```

### **3. Add the Gemini Plugin**
By default, the `llm` tool needs a plugin to communicate with Google’s Gemini models.

```bash
# This plugin enables the LLM tool to interface with Google's API
llm install llm-gemini
```

---

## 🔑 Part 2: Gemini API Setup
To use Gemini, you must provide a unique API key so Google can authenticate your requests.

### **1. Generate Your Key**
1. Visit **[Google AI Studio](https://aistudio.google.com/welcome)**.
2. Sign in with a personal Gmail account
3. Click on **"Create API key"**.
4. Select a project (or create a new one) and click **"Generate API key"**.
5. **Copy** the generated key to your clipboard.

### **2. Configure the Key in Ubuntu**
Return to your Ubuntu terminal to securely store the key. Git/LLM handles this by storing it in a local configuration file.


1. Type the following command:
```bash
llm keys set gemini
```

2. When prompted, **paste** your API key. 

> [!IMPORTANT]
> **Note:** The cursor will not move, and the key will not be visible as you paste it for security reasons. Just paste and press **Enter**.

---

## ✅ Part 3: Verification
Your Gemini API is now configured! You can test it by asking a question directly from the command line:



```bash
# Running a test query to verify authentication
llm -m gemini-2.5-flash "Hello, how are you?"
```
---
---

# 🛠️ Hands-On: Github CLI and Python Environment
**Chapter 1 | Week 1 | Session 4**

This practical session covers the installation of the UV package manager, setting up the Github CLI tool, authomation of Github. 
---

## **Part 1: Automatic Github Environment setup**
The `uv init` command is the "Big Bang" for your Python projects. It is a scaffolding tool that sets up a professional, clean project structure in milliseconds, ensuring you follow best practices from the very first second.

### **📦 What is Created?**
When you run `uv init` inside a folder, it generates four essential files:

* **`pyproject.toml`**: The "Brain." This file stores your project metadata (name, version) and tracks all the libraries you install.
* **`.gitignore`**: The "Filter." It automatically tells Git to ignore junk files like your virtual environment (`.venv`) and Python cache.
* **`hello.py`**: The "Starter." A simple "Hello World" script so you can verify everything is working immediately.
* **`.python-version`**: The "Anchor." It tells `uv` exactly which version of Python should be used for this project to ensure consistency.

---

## **Part 2: 🛠️ GitHub CLI (`gh`) Command List**

The GitHub CLI allows you to manage your repositories without leaving the terminal. It is significantly faster than using the web interface for creating and managing projects.

---

### **1. Authentication**
Before you can use `gh`, you must link your terminal to your GitHub account.
* **Command:** `gh auth login`
* **Workflow:** 1. Select `GitHub.com`.
    2. Choose `HTTPS`.
    3. Select `Yes` to authenticate with your GitHub credentials.
    4. Choose `Login with a web browser` and paste the one-time code provided.

---

### **2. Creating a Remote Repository**
Instead of creating a repo on the website and then cloning it, you can create it directly from your local project folder.
* **Command:** `gh repo create`
* **Example Workflow:**
    ```bash
    git init
    git add .
    git commit -m "initial commit"
    
    # Now use GH to push to the cloud
    gh repo create my-repo-name --public --source=. --remote=origin --push
    ```

* **Interactive Choices:** It will ask if you want to push the current folder to GitHub, set the name, and whether it should be `Public` or `Private`.

---

### **3. Opening Your Project Online**
If you need to check your Actions, Issues, or look at your code on the web:
* **Command:** `gh repo view --web`
* **Effect:** Instantly opens the current repository's GitHub page in your default browser.

---

### **4. Standard Git Integration**
These commands are often used right before or after the `gh` commands to manage your local code:

| Command | Purpose |
| :--- | :--- |
| `git init` | Starts a new Git project locally. |
| `git add .` | "Stages" all your files to be saved. |
| `git commit -m "message"` | Saves a snapshot of your code locally. |
| `git status` | Shows which files are changed but not yet saved. |

---
---

# 🔐 Hands-On: GitHub SSH Setup Guide (Ubuntu WSL)
**Chapter 1 | Week 1 | Session 5**

Using SSH (Secure Shell) allows you to securely communicate with GitHub without entering your password or token every time you push code.

Refer this link for stepup process [SSH setup](https://github.com/Jivraj-18/live-sessions-tds-09-2025/blob/main/git-setup-24-09-2025.md)
---

### **Step 1: Generate a New SSH Key**
Open your Ubuntu WSL terminal and run the following command. Replace the email with your actual GitHub email address.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

* **File Location:** When prompted to "Enter a file in which to save the key," simply press **Enter** (it will save to `~/.ssh/id_ed25519`).
* **Passphrase:** Press **Enter** twice for no passphrase (convenient) or type a secret password for extra security.


### **Step 2: Start the SSH Agent**
The SSH agent is a background process that holds your keys so you don't have to re-enter passphrases manually every time you use them.



```bash
# Start the agent
eval "$(ssh-agent -s)"

# Add your private key to the agent
ssh-add ~/.ssh/id_ed25519
```

### **Step 3: Add the Public Key to GitHub**
You need to provide GitHub with your **Public Key** so it can recognize your computer.


1. **Display and Copy the key:**
```bash
   cat ~/.ssh/id_ed25519.pub
```
2. **Go to GitHub:**
    * Log in to **[GitHub.com](https://github.com)**.
    * Go to **Settings** (top right profile icon).
    * Click **SSH and GPG keys** in the left sidebar.
    * Click the green **New SSH Key** button.



* **Paste the Key:**
    * **Title:** Give it a name like "My WSL Ubuntu".
    * **Key:** Paste the text you copied from your terminal.
    * Click **Add SSH Key**.

---

### **Step 4: Test the Connection**
Finally, verify that Ubuntu can talk to GitHub:

```bash
ssh -T git@github.com
```

Note: If it asks "Are you sure you want to continue connecting?", type yes and press Enter.

    Success: You should see: "Hi [YourUsername]! You've successfully authenticated..."

💡 **Pro Tip:** Update Your Remote URL

If you previously cloned a repository using HTTPS, you need to switch it to SSH to stop it from asking for a password:
Bash

# Check current URL
git remote -v

# Change to SSH (Replace <user>/<repo> with yours)
git remote set-url origin git@github.com:<user>/<repo>.git