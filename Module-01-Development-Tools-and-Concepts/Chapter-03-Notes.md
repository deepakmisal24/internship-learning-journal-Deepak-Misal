# 🛠️ Session 3: Hypervisors, path, UV, LLM and API keys
**Chapter 1 | Week 1 | Session 3**

This session bridges the gap between your local computer and the cloud by establishing a robust AI development environment.

---

## **1. 🏗️ Understanding Hypervisors**

A **Hypervisor**, also known as a **Virtual Machine Monitor (VMM)**, is a specialized layer of software, firmware, or hardware that sits between a physical machine's hardware and its operating systems.

![Hypervisor flowchart](hypervisor.png)

> **Analogy:** If your computer is an office building, the **Hypervisor is the Building Manager**. It is responsible for dividing the building's resources (CPU, RAM, and Storage) among different tenants (Virtual Machines) to ensure they can all work simultaneously without interfering with each other.



---

## 🏗️ The Two Main Types of Hypervisors

Hypervisors are categorized based on where they sit in the system stack. 

### **Type 1: Bare-Metal Hypervisors**
These run directly on the host's physical hardware. There is no traditional operating system (like Windows or Linux) underneath them. They essentially *act* as the operating system for the hardware.

* **Best for:** Enterprise data centers and cloud environments (AWS, Azure).
* **Pros:** High performance, low latency, and superior security because the attack surface is tiny.
* **Examples:** VMware ESXi, Microsoft Hyper-V (running on Windows Server), and KVM (Linux-based).

### **Type 2: Hosted Hypervisors**
These run as an application on top of an existing operating system. The "host" OS (like your Windows 11 or macOS) manages the hardware, and the hypervisor asks the host OS for resources.

* **Best for:** Developers, testers, and personal use.
* **Pros:** Easy to install, user-friendly, and doesn't require wiping your computer.
* **Examples:** Oracle VirtualBox, VMware Workstation, and Parallels Desktop.



---

## ⚙️ How a Hypervisor Works (The Architecture)

A hypervisor performs three critical functions to make virtualization possible:

* **Abstraction:** It hides the physical hardware details from the Virtual Machines (VMs). The VM "thinks" it has its own dedicated Intel CPU and 8GB of RAM, but it’s actually just a slice of the real hardware.
* **Isolation:** This is the most important role. If one VM crashes or gets a virus, the hypervisor ensures it doesn't spread to the host or other VMs. Each VM is a "sandbox."
* **Scheduling:** The hypervisor acts as a traffic controller. It decides which VM gets to use the CPU at any given millisecond, ensuring no single VM hog-ties the entire system.



---

## 📊 Quick Comparison

| Feature | Type 1 (Bare-Metal) | Type 2 (Hosted) |
| :--- | :--- | :--- |
| **Runs On** | Physical Hardware | Host OS (Windows/Mac/Linux) |
| **Performance** | High (Direct Access) | Lower (OS Overhead) |
| **Security** | Stronger Isolation | Dependent on Host OS |
| **Setup** | Complex | Simple Application Install |

---

## **✅ Why Use a Hypervisor?**

Using a hypervisor provides several strategic advantages that transform how hardware is managed and utilized.

---

### **1. Resource Efficiency (Server Consolidation)**
Instead of having five under-utilized physical servers, you can run five Virtual Machines (VMs) on one powerful server. This maximizes your return on investment by ensuring that hardware isn't sitting idle.



### **2. Legacy Support**
Hypervisors allow you to run an old Windows XP application inside a VM on a modern Windows 11 machine. This is critical for businesses that rely on older software that won't run on modern operating systems.



### **3. Disaster Recovery**
Since VMs are essentially just "files" on a disk, they are incredibly easy to back up. You can take a **snapshot** (a point-in-time save) of a VM or clone it to another physical machine in seconds if something goes wrong.



### **4. Portability**
Hypervisors provide "hardware independence." You can move a VM from your local laptop to a server in the cloud (like AWS or Azure) without having to change any of the software settings or drivers inside the VM.


---

## **2. Paths: Absolute vs. Relative (The Address System)**
Paths are just directions to a specific room in the building.
### **1. Absolute Path**
An **absolute path** is the complete and exact address of a file starting from the **root directory** (the very top of the system).

* **Key Indicator:** It *always* starts with a forward slash (`/`).
* **Behavior:** It works the same regardless of where you are currently located in the terminal.
* **Example:** `/home/user/Documents/report.txt`

If you want to view a file named `hosts` located in the system's configuration folder, you would type:

```bash
cat /etc/hosts
```
### **2. Relative Path**
A **relative path** specifies a location in relation to your **Present Working Directory (pwd)**—the folder you are currently "standing" in.

* **Key Indicator:** It *never* starts with a forward slash (`/`).
* **Behavior:** It only works if you are in the correct starting location.
* **Special Symbols:**
    * `.` (Single dot): Refers to the **current** directory.
    * `..` (Double dot): Refers to the **parent** (one level up) directory.
    * `~` (Tilde): Shortcut for your **home** directory (e.g., `/home/username`).


---

## **3. Mounting and the `/mnt` Folder (The Bridge)**
Imagine there is a second building next door (Windows). **Mounting** is like building a covered walkway (bridge) between the two.



The **`/mnt`** folder in Linux is that bridge. In **WSL**, this is how you access your Windows files from inside the Linux terminal.

* **The Mount Point:** A directory (like `/mnt/c`) that serves as the entry point for a separate drive.
* **The Unified Tree:** Unlike Windows (which uses `C:` or `D:`), Linux puts everything into one big "tree" starting from `/`.
* **Example:** To see your Windows files, you "cross the bridge" by going to `/mnt/c`.

---

## **4. Essential Commands (The Office Tools)**
* **`ls` (Look Around):** Turning on the lights to see what files are in the room.
* **`touch` (Place a Folder):** Placing a new, empty file folder on a desk.
* **`cd` (Walk):** Actually walking from one room to another.
* **`vi` (The Notebook):** Opening a notebook to write or edit notes inside a file.


| Command | Action |
| :--- | :--- |
| `ls` | **List:** Shows files and folders in the current directory. |
| `touch <filename>` | **Create:** Generates a new empty file. |
| `cd <path>` | **Change Directory:** Moves you to a different folder. |
| `vi <filename>` | **Edit:** Opens the Vim text editor to modify a file. |


---

## **5. The `/bin` Folder (The Utility Closet)**
The **`/bin`** folder is the **Utility Closet** of your Linux system. It contains the "binaries" (executable programs) for the most fundamental commands required for the system to boot and run.



* **Essential Tools:** It stores commands like `ls`, `cp`, `mv`, and `cat`.
* **System-Wide Access:** These tools are available to all users and are reachable even if other parts of the system are not yet mounted.
* **No Extensions:** Unlike Windows (where apps end in `.exe`), Linux binaries in `/bin` usually have no file extension.

---

## **6. UV, LLM, and API (The Smart Assistant)**
### **1. UV (The Rapid Delivery Service)**
**UV** is an extremely fast Python package manager and tool installer written in Rust. In the world of Python, we’ve used `pip` for decades, but it can be slow and messy.

* **The Analogy:** Think of **UV** as a high-speed, automated delivery drone. While `pip` might take minutes to find and install a tool, **UV** does it in milliseconds.
* **What it does for you:** It handles the "boring stuff"—installing the LLM tool, managing different Python versions, and making sure tools don't interfere with each other.


### **2. LLM (The AI Interface)**
While "**LLM**" usually stands for Large Language Model (like GPT-4), here it refers to a specific **Command Line Interface (CLI)** tool.



* **The Analogy:** If ChatGPT is a fancy website, the `llm` tool is a "**walkie-talkie**" for your terminal. It allows you to send text to an AI and get a response back without ever leaving your Ubuntu window.
* **Why use a CLI tool?** It’s built for **automation**. You can pipe the contents of a file directly into the AI which is much faster than copying and pasting into a browser.


### **3. API (The Digital Keycard)**
An **API (Application Programming Interface)** is a set of rules that allows two different pieces of software to talk to each other. In this context, we are talking about **API Keys**.

* **The Analogy:** To talk to a smart consultant (Gemini or OpenAI), you need a **Keycard**. When you send a request via the `llm` tool, you "swipe" your API key. Google or OpenAI checks that key; if it's valid, they let the AI answer you.
* **The Handshake:**
    1.  **Your Terminal:** "Hey Gemini, here is a question + my API Key."
    2.  **Google's Server:** "Key is valid. Here is the answer."
    3.  **Your Terminal:** Displays the answer to you.