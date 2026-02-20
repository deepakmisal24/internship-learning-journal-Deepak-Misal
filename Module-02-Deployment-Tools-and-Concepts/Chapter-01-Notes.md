# Containerization & Local AI Infrastructure

This guide provides a detailed breakdown of containerization concepts, management tools, and the integration of local LLMs like Ollama within a development ecosystem.

---

## 1. Core Concepts: Containerization & Docker
**Containerization** is the process of packaging an application together with its dependencies (libraries, configuration files, and runtime) into a single "image." This ensures the application runs consistently regardless of the host environment.

* **Docker:** The industry-standard platform for building and running containers. It uses a **Daemon** (background process) to manage images and container lifecycles.
* **Key Advantage:** It solves the "works on my machine" dilemma by isolating the application from the underlying operating system.

## 2. Podman & Pods
**Podman** is a "daemonless" container engine designed as a drop-in replacement for Docker.

* **Daemonless Architecture:** Unlike Docker, Podman doesn't require a background service with root privileges, making it more secure.
* **Pods:** A concept originating from Kubernetes. A **Pod** is a group of one or more containers that share the same network stack and storage volumes. 
    * *Analogy:* If a container is a single tenant, a Pod is an apartment where everyone shares the same front door and address.

## 3. Virtual Machines (VMs) vs. Pods
| Feature | Virtual Machine (VM) | Pod (Containers) |
| :--- | :--- | :--- |
| **Architecture** | Includes a full Guest OS | Shares the Host OS Kernel |
| **Isolation** | Strong (Hardware level) | Process-level (Namespace/Cgroups) |
| **Size** | Gigabytes (GB) | Megabytes (MB) |
| **Startup** | Minutes | Seconds |

---

## 4. Persistent Storage (Volume Mounting)
By default, containers are **ephemeral**—any data created inside them is lost when the container is deleted. To save data (like database records or AI models), we use **Volumes**.

* **Bind Mounts:** Maps a specific path on your physical computer (Host) to a path inside the container.
* **Docker Example:** `-v /Users/me/data:/app/data`
    * Any file placed in the host folder is immediately visible to the container and persists after the container stops.

---

## 5. Ollama: Local LLMs
**Ollama** allows you to run Large Language Models (like Llama 3 or Mistral) locally on your own hardware.

* **Docker Hub:** The [official image](https://hub.docker.com/r/ollama/ollama) (note: `alpine/ollama` is often a community variant; the official is `ollama/ollama`) allows for easy deployment.
* **Ollama API:** Once running, Ollama provides a REST API on port `11434`. 
    * **Endpoint:** `POST /api/generate`
    * **Payload:** `{"model": "llama3", "prompt": "Explain Quantum Physics"}`

---

## 6. Networking: Flask, JupyterLab, & Ollama
When running a multi-container setup (e.g., a Jupyter notebook and a Flask API connecting to Ollama), you must handle container-to-container networking.

### Docker Compose Setup
Using `docker-compose.yml` automatically creates a private network where containers can "see" each other by their service names.

```yaml
services:
  ollama:
    image: ollama/ollama
    volumes:
      - ./ollama_storage:/root/.ollama

  jupyter:
    image: jupyter/scipy-notebook
    ports:
      - "8888:8888"

  flask_api:
    build: ./my-flask-app
    ports:
      - "5000:5000"
```

How they communicate:
1. Inside the Network: Flask doesn't use `localhost:11434` (that refers to itself). It uses the service name.
2. Endpoint: In your Python code, you would call `http://ollama:11434/api/generate`.

### A Simple Flask Example
To connect your Flask app to Ollama:

```bash

import requestsfrom flask import Flask, request

app = Flask(__name__)@app.route('/ask')def ask_ai():
    prompt = request.args.get('q')
    # Notice the URL uses 'ollama' as the hostname
    response = requests.post("http://ollama:11434/api/generate", 
                             json={"model": "llama3", "prompt": prompt, "stream": False})
    return response.json()['response']
```