# 🛠️ Session 2: Hypervisor Deep Dive & Git Basics
**Chapter 1 | Week 1 | Session 2**

This session explores the technical "why" behind **WSL 2**, its architectural advantages over traditional Virtual Machines, and the core principles of **Version Control Systems (VCS)**.

---

## 🐙 Introduction to Version Control (Git)
The video introduces **Git** as an "Undo" button for developers that persists even after closing the editor. Unlike standard undo functions, Git allows you to track changes across weeks or months of work.

### **The Git Lifecycle**
To manage your code effectively, you follow a specific lifecycle:

* **Initialize (`git init`):** Creates a hidden `.git` folder in your directory to start tracking history.
* **Checkpoints (Commits):** These act as "save-points" in a game. If you break your code, you can "teleport" back to a previous commit (checkpoint).



### **GitHub vs. Git**
It is important to distinguish between the tool and the platform:
* **Git:** The local software installed in your WSL/Ubuntu environment that manages your history.
* **GitHub:** The cloud website (like a specialized Google Drive) where you "push" your local history for backup and collaboration.

---
## 🐙 1. Git: The Local Time Machine
**Git** is a Distributed Version Control System (VCS) that resides entirely on your local machine (within your WSL/Ubuntu environment). It acts as an "Undo" button for developers that persists even after closing your editor.

### **The Three States of Git**
Git manages files across three distinct areas. Understanding this flow is essential for maintaining a clean project history:

1.  **Working Directory:** Your active, unstaged files.
2.  **Staging Area (Index):** A "drafting" area where you group changes (`git add`).
3.  **Local Repository:** The permanent history of your project (`git commit`).



### **Snapshots, Not Backups**
Unlike traditional methods that save multiple file versions (e.g., `Project_v1`, `Project_v2`), Git saves **snapshots** of your entire project directory at a specific point in time.

---

## ☁️ 2. GitHub: The Social Cloud
While Git is the engine, **GitHub** is the cloud-based "garage" where you store and share that engine.

* **Collaboration:** Enables multiple engineers to work on the same codebase simultaneously.
* **Source of Truth:** Acts as a remote backup. If your local WSL environment crashes, your work remains safe on GitHub.
* **Authentication:** Uses **SSH Keys** or **Personal Access Tokens (PATs)** to securely verify your identity when pushing code.



---

## 🚀 3. Deployment: Going Live
**Deployment** is the process of moving code from GitHub to a live server for user access.

* **Static Hosting:** Ideal for HTML/CSS via **GitHub Pages**.
* **Dynamic Hosting:** Essential for Data Science apps via **Vercel**, **Hugging Face Spaces**, or **Render**.
* **The "Bridge":** These platforms "watch" your repository. When you push a commit, they automatically pull the new code and restart the application.

---

## ⚙️ 4. CI/CD: The Automated Pipeline
CI/CD provides the "automation" layer connecting GitHub to your final deployment.



### **Continuous Integration (CI)**
Automated scripts run on every push to check for quality:
* **Testing:** Checks Python code for syntax errors.
* **Building:** Verifies that the project builds without crashing.

### **Continuous Deployment (CD)**
Triggered only if CI tests pass:
* **Automation:** Pushes verified code to servers (Vercel, Docker, etc.).
* **Zero Downtime:** Ensures the current version stays live until the new one is fully ready.

---

## 📊 Summary of the Flow

1.  **Code:** Write code in your **WSL Ubuntu terminal** (Local).
2.  **Commit:** Save snapshots locally using **Git**.
3.  **Push:** Send the local history to **GitHub**.
4.  **Test:** **GitHub Actions (CI)** automatically runs tests.
5.  **Deploy:** **Deployment (CD)** updates your live website or API automatically.

---