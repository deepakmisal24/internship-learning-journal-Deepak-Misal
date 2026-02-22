# **Docker, Podman, Ollama, Flask**
**Week 2 | Session 1**

* **Docker:** A leading platform that uses OS-level virtualization to deliver software in packages called containers, ensuring consistency across different computing environments.
* **Containerization:** The process of packaging an application together with its required libraries, frameworks, and dependencies so that it runs reliably in any environment.
* **Podman:** A daemonless, open-source container engine used to develop, manage, and run OCI containers, designed as a more secure, rootless alternative to Docker.
* **Pod:** The smallest execution unit in Podman or Kubernetes, consisting of one or more containers that share the same network namespace and storage resources.
* **Virtual Machine vs. Pod:** A VM simulates an entire hardware system and includes a full guest OS, whereas a Pod shares the host's OS kernel, making it significantly more lightweight and faster to start.
* **Persistent Storage with Volume Mounting:** A method of linking a directory on the host machine to a directory inside a container so that data remains saved even after the container is deleted.
* **Ollama:** A framework designed to run large language models (LLMs) locally, often deployed via lightweight images like `alpine/ollama` to minimize resource overhead.
* **Ollama API:** A local interface that allows external applications to communicate with running AI models programmatically via HTTP requests.
* **Flask:** A lightweight Python web framework used to build web applications and APIs, often serving as the "bridge" between a user interface and a backend AI model.

---

# **Quick Reference: Web Development & Hosting**
**Week 2 | Session 2**

* **GitHub Pages:** A static site hosting service that pulls HTML, CSS, and JavaScript directly from a GitHub repository to publish websites for free.
* **FastAPI:** A modern, high-performance Python web framework used for building APIs based on standard Python type hints and asynchronous programming.
* **FastAPI vs. Flask:** FastAPI is an asynchronous, high-speed framework with automatic data validation and documentation, whereas Flask is a simpler, synchronous micro-framework that often requires external libraries for similar features.
* **Uvicorn:** A lightning-fast ASGI server implementation that serves as the engine to run asynchronous Python web applications like FastAPI.
* **Vercel:** A cloud platform designed for hosting frontend frameworks and serverless functions that provides instant deployment and automatic scaling directly from Git repositories.
* **ngrok:** A cross-platform application that exposes local development servers to the internet by creating a secure, encrypted tunnel from a public URL to a specific port on your machine
### 🛠️ Vercel CLI: Useful Commands Summary

The following table summarizes the most common commands used to manage projects and deployments directly from your terminal.

| Command | Action |
| :--- | :--- |
| `vercel` | Deploy a **Preview** version of the current directory. |
| `vercel --prod` | Deploy the current code directly to the **Production** environment. |
| `vercel login` | Authenticate your terminal session with your Vercel account. |
| `vercel link` | Connect your local folder to an existing Vercel project without deploying. |
| `vercel env add <name>` | Securely add a new **Environment Variable** (e.g., API keys) to your project. |
| `vercel env pull` | Download your cloud environment variables into a local `.env` file for testing. |
| `vercel dev` | Start a **local development server** that replicates the Vercel environment. |
| `vercel logs` | Stream live build and runtime logs to debug your application in real-time. |
| `vercel remove <name>` | Permanently delete a project and its associated deployments from Vercel. |

---