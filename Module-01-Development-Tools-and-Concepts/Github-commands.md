# 🛠️ The Ultimate Git & GitHub Command Roadmap

This structure compiles all the essential commands you've learned into a logical workflow, from initial installation to advanced cloud automation.

---

### **Phase 1: Environment Setup**
Run these once to prepare your Ubuntu (WSL) system and identify yourself to the network.



| Category | Command | Description |
| :--- | :--- | :--- |
| **Installation** | `sudo apt update && sudo apt install git -y` | Updates packages and installs Git. |
| **Verification** | `git --version` | Checks if Git is installed correctly. |
| **Identity** | `git config --global user.name "Your Name"` | Sets your display name for commits. |
| **Identity** | `git config --global user.email "email@example.com"` | Links your commits to your GitHub account. |

---

### **Phase 2: The Local Workflow (Save Points)**
These commands are used daily within your project folder to track changes.



1.  **Initialize:** `git init`  
    *Run once per project to start tracking.*
2.  **Stage:** `git add .`  
    *Prepares all changed files for a snapshot.*
3.  **Commit:** `git commit -m "Your message"`  
    *Saves the snapshot to your local history.*

---

### **Phase 3: The Remote Bridge (Connecting to Cloud)**
Manage the connection between your local machine and GitHub.



* **View Connections:** `git remote -v`
* **Link to GitHub:** `git remote add origin git@github.com:user/repo.git`
* **Switch to SSH:** `git remote set-url origin git@github.com:user/repo.git`
* **The Final Upload:** `git push -u origin main`

---

### **Phase 4: GitHub CLI (`gh`) Automation**
Streamline your workflow by bypassing the GitHub website entirely.



* **Login:** `gh auth login`
* **One-Step Repo Creation:** `gh repo create my-repo --public --source=. --remote=origin --push`  
    *(This creates the repo on GitHub, links it locally, and pushes your code in one go.)*

---

### **Phase 5: Secure Authentication (SSH)**
The professional way to handle security without typing passwords.

| Step | Command |
| :--- | :--- |
| **1. Generate** | `ssh-keygen -t ed25519 -C "email@example.com"` |
| **2. Start Agent** | `eval "$(ssh-agent -s)"` |
| **3. Add Key** | `ssh-add ~/.ssh/id_ed25519` |
| **4. View Public Key** | `cat ~/.ssh/id_ed25519.pub` (Copy this to GitHub Settings) |
| **5. Test** | `ssh -T git@github.com` |

---

> [!TIP]
> **Daily Routine:** `git add .` → `git commit -m "..."` → `git push`.  
> Always run `git status` if you are unsure which phase you are currently in!