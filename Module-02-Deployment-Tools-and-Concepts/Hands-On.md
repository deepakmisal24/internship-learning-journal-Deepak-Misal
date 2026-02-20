
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