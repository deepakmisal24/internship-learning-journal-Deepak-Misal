
## **Setup of Git**
### **Install Git inside Ubuntu (WSL)**
Open your Ubuntu terminal and execute the following commands to ensure the package manager is current and Git is installed:

```bash
# Update your package list
sudo apt update

# Install Git
sudo apt install git -y

# Verify the installation
git --version
```

---

### **Configure your Git Identity**
Git requires a registered identity to label "save-points" (commits). This information is attached to every change you make.

```bash
# Set global configuration
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## **Commands for pushing into Github**

**Initialize Git** 

1. Open your project folder in **VS Code** (`File > Open Folder`).
2. Open the **Integrated Terminal** .
3. Run the initialization command:

[!Note:]
Intitialization of git is required once per project
```bash
git init
```

**Stage files**
To add the list of files to push. Use **add** followed by the files to be push. If current directory the use the following code
```bash
git add .
```

**Comment the changes**
TO create a history (snapsshot) of the changes made we **commit** using.
```bash
git commit -m "Description of the changes for future reference"
```

### **The Final Push**
Upload your local commits to the remote "origin" server on the "main" branch.

```bash
# Use the -u flag the first time to track the remote branch
git push -u origin main
```

---

## **Setup of Git Command Line Interface(CLI)**
Before you can use `gh`, you must link your terminal to your GitHub account.
```bash
gh auth login
```

#### **2. Creating a Remote Repository**
Instead of creating a repo on the website and then cloning it, you can create it directly from your local project folder.