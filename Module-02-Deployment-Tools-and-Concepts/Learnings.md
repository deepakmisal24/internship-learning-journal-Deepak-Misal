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
