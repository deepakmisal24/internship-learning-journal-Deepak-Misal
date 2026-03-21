# **Docker, Podman, Ollama, Flask**
**Week 2 | Session 1**

## **Installation and Setup**
### **1. Install Podman and Dependencies**

First, update your package list and install Podman along with the QEMU emulator for x86 architecture support.
```Bash
sudo apt update
sudo apt install -y podman qemu-system-x86
podman machine init
podman machine start #Sometimes it might not work
sudo chmod 666 /dev/kvm #run this in that case. This will raise a error "/" is not shared mount then
sudo mount --make-rshared / # to overcome previous error
```

### **2. Pull the Jupyter Image**

Download the official base notebook image from the Quay.io registry.

```Bash
podman pull quay.io/jupyter/base-notebook
```

#### List images:
```bash
podman images
```
#### List running containers:
```bash
podman ps
```
#### List all containers:
```bash
podman ps -a
```


## **🛠️ Basic Container Management**
#### **Permission Handling (chmod)**
The container might not have permission to write to your local folder. So, giving full permissions to the work directory to prevent "Permission Denied" errors when saving notebooks.
```Bash
mkdir jupyter_work
# Give full read/write/execute permissions to your local work folder
chmod 777 ~/jupyter-work
```

#### Start the Container
Run the container in detached mode and map the internal port to your local machine.

```Bash
podman run -d --name jupyter_server -p 8888:8888 quay.io/jupyter/base-notebook
```

#### Accessing the Environment
1. **Check Logs:** You will need to see the logs to retrieve the login token for the first session.
``` Bash
    podman logs jupyter_server
```
2. Open Browser: Navigate to http://localhost:8888.

#### **Stopping and Cleanup**
To stop and remove the container and its associated image:
```Bash

# Stop the running container
podman stop jupyter_server

# Remove the container
podman rm jupyter_server

# Delete the image from local storage
podman rmi quay.io/jupyter/base-notebook

```

## **💾 Persistent Storage (Volume Mount)**

By default, data created inside a container is lost when the container is removed. Use the following command to map a folder on your host machine to the container, ensuring your work is saved permanently.
```Bash

podman run -d \  --name jupyter-server \  -p 8888:8888 \  -v ~/jupyter-work:/home/jovyan/work \  quay.io/jupyter/base-notebook
```
![Jupyter notebook in podman container all commands](podman-container-all-cmd.png)


## **Ollama podman: installation and setup**

### Pull ollama images
```bash
podman pull docker.io/alpine/ollama:0.12.9
podman run -d --name ollama docker.io/alpine/ollama
```
### Install model and test
```bash
podman exec -it ollama sh #sh to invoke shell inside the container
```

### Download models in Ollama
```bash
ollama run <"Model-name:paramters"> #Ex: gemma3:270m
#Gemma 3 model is pulled and ready to use.
```

### Different commands in Ollama
```bash
ollama
```

## **Network between ollama and jupylab**
s1: Open the [site]https://ollama.readthedocs.io/en/api/
s2: Scroll to find **Request (No streaming)** then copy the **curl command**
s3: create a network
```bash
podman network create ai-network
```
s4: Run the network
```bash
podman run -d --name ollama --network ai -p 11434:11434 docker.io/alpine/ollama
```

# **Github Pages set-up**
**Week 2 | Session 2**

GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files directly from a repository on GitHub and publishes a website.

---

## 🛠️ Step-by-Step Setup

### 1. Create a Repository
1. Log in to your GitHub account.
2. Click the **+** icon in the top right and select **New repository**.
3. **Repository Name:** - For a *Project Site*: Use any name (e.g., `my-portfolio`).
   - For a *User Site*: Use `username.github.io` (replace `username` with your actual GitHub username).
4. Set the visibility to **Public**.
5. Check **Add a README file**.
6. Click **Create repository**.

### 2. Add Your Website Content
1. Inside your repository, click **Add file** > **Create new file**.
2. Name the file `index.html`. This **must** be in the root directory.
3. Paste the following basic HTML code:
```bash
    <!DOCTYPE html>
   <html>
   <head>
       <title>My GitHub Page</title>
   </head>
   <body>
       <h1>Successfully Deployed!</h1>
       <p>Welcome to my site hosted via GitHub Pages.</p>
   </body>
   </html>
```
4. Commit and Push these changes to the `main` branch.

### 3. Enable GitHub Pages in Settings
1. Navigate to the Settings tab of your repository.
2. On the left-hand sidebar, under the "Code and automation" section, click on **Pages**.
3. Under Build and deployment > Source, ensure "Deploy from a branch" is selected.
4.  Under Branch, select `main` (or whichever branch your code is on) and the folder (usually `/ (root)`).
5.  Click Save.

### 4: Verify the Live Site
1. Wait a minute or two for the GitHub Actions runner to finish the build.
2. At the top of the GitHub Pages settings page, you will see a banner saying: "Your site is live at..." with a URL.
3.  Click the link to view your website.

---

## **Deployment of project using Vercel**

# Step-by-Step Vercel Deployment Guide

### 1. Prepare Your Project Files
Ensure your root directory contains these three essential files:
* **`app.py`**: Your main application logic.
* **`requirements.txt`**: List of libraries (remove `uvicorn` as Vercel provides the server).
* **`vercel.json`**: Routing configuration.

### 2. Configure `vercel.json`
Create a `vercel.json` file in your root folder with the following code:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "app.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "app.py"
    }
  ]
}
```
### 3. Install & Login to Vercel CLI

Open your terminal and run:
```Bash

# Install the CLI globally
npm install -g vercel

# Authenticate your account
vercel login
```
### 4. Initialize the Project

Run the initial setup command and follow the interactive prompts:
```Bash

vercel
```
* Set up and deploy? Y

* Which scope? [Select your username]

* Link to existing project? N

* Project Name: [Give your project a name]

* In which directory? ./

* Modify settings? N

### 5. Production Deployment

Once the preview is ready, push your project to the live production environment:
```Bash

vercel --prod
```

---

# **Github and huggingface Codespace set-up**
**Week 2 | Session 3**

## 1. GitHub Codespaces Setup
### Quick Setup Options
* **From the GitHub UI:** Go to your repository and click **Code** → **Codespaces** → **New codespace**. Pick the branch and machine specs (2–32 cores, 8–64 GB RAM), then click **Create codespace**.
* **In Visual Studio Code:** Press `Ctrl+Shift+P`, choose `Codespaces: Create New Codespace`, and follow the prompts.
* **Via GitHub CLI:**
    ```bash
    gh auth login
    gh codespace create --repo OWNER/REPO
    gh codespace list    # List all codespaces
    gh codespace code    # Open in your local VS Code
    gh codespace ssh     # SSH into the codespace
    ```

## 2. devcontainer.json
The `.devcontainer/devcontainer.json` file is the configuration heart of your codespace. It tells GitHub exactly how to build your development environment.

* **Key Attributes:**
    * **`image` or `dockerFile`**: Defines the base OS or custom Docker image to use.
    * **`features`**: Installs common tools (like Node.js, Python, or Docker-in-Docker) with a single line.
    * **`postCreateCommand`**: A shell command (e.g., `pip install -r requirements.txt`) that runs automatically once the container is created.
    * **`forwardPorts`**: Maps ports from the cloud machine to your local browser so you can preview apps.

## 3. Hugging Face Spaces
Spaces allow you to host ML demo apps for free. When initializing a Space, you must choose an SDK based on your project:
* **Gradio (Default):** The fastest way to build an interface for an ML model using only Python.
* **Streamlit:** A Python library for creating complex, interactive data dashboards.
* **Static HTML:** For hosting simple, front-end only interfaces.
* **Docker:** The most flexible option; allows you to provide a custom `Dockerfile` to run any language or complex environment.

### Setting up a Space
1. Visit [huggingface.co/new-space](https://huggingface.co/new-space).
2. Fill up the **Name** and **License**.
3. Select the **Space SDK** (Gradio, Streamlit, Static, or Docker).
4. Select the **Space Hardware** (CPU/GPU options).
5. Click **Create Space**.

### Manual Deployment Process
1. **Clone Repository:** `git clone https://huggingface.co/spaces/your-username/your-space-name`
2. **Add Files:** Create your application files in your local repository.
3. **Deploy:**
    ```bash
    git add .
    git commit -m "Initial deployment"
    git push
    ```

---

## 4. GitHub Actions
**GitHub Actions** is a platform to automate your software development workflow. It allows you to run scripts automatically based on repository triggers like a `push` or a `pull_request`.



## 5. Use Cases (CI/CD)
GitHub Actions is primarily used for:
* **Continuous Integration (CI):** Every time you push code, Actions can run your unit tests and linting to ensure no bugs are introduced.
* **Continuous Deployment (CD):** Automatically push your updated code and model weights to Hugging Face Spaces as soon as they pass tests.

### **Workflow setup**
Create a file at `.github/workflow/deploy.yml`

```yaml
name: Sync to Hugging Face
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
          lfs: true
      - name: Push to HF
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: git push --force https://USERNAME:$HF_TOKEN@huggingface.co/spaces/USERNAME/SPACE_NAME main
```

---

# **FastAPI set-up**
**Week 2 | Session 4**

## 1. Installation
```bash
# Create project folder
mkdir FastAPI_Project
cd FastAPI_Project

# Setup Virtual Environment
python -m venv venv
source venv\Scripts\activate

# Install core packages
pip install fastapi uvicorn python-multipart

```
## 2. Running the Server
```bash
uvicorn app:app --reload
```

* main: The filename (main.py).

* app: The FastAPI instance variable inside the file.

* --reload: Automatically restarts the server on code changes.
1. Right-click on the port link `http://127.0.0.1:8000`
2. To check the changes and run the program`http://127.0.0.1:8000/docs`

![app.py](Airowire-Internship\FastAPI\venv\app.py)