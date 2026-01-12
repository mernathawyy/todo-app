
# todo-app
=======
# Todos-nodejs
=======


## Documentation
This project demonstrates a complete DevOps workflow including CI, configuration management, containerization, auto-deployment, and GitOps using ArgoCD.

## Part 1: CI Pipeline & Dockerization (30 Points)
 **Objective**

Containerize the Todo Node.js application and build a CI pipeline that pushes the Docker image to a private registry.

### Step 1: Clone the Application Repository

The application repository was cloned from GitHub:

`git clone https://github.com/Ankit6098/Todo-List-nodejs.git `

`cd Todo-List-nodejs `


### Step 2: Configure MongoDB Database

A personal MongoDB database was created and configured in the .env file.

Updated MONGO_URI

Updated application port if needed

**Example:**

MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/todo
PORT=4000


### Step 3: Dockerize the Application

A Dockerfile was created to containerize the Node.js application.

**Key points:**

Used official Node.js base image

Installed dependencies

Exposed application port

Used npm start as entrypoint
```bash
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 4000
CMD ["npm", "start"]
```


### Step 4: Build and Test Docker Image Locally

The Docker image was built and tested locally to ensure it works correctly.

docker build -t todo-app .
docker run -p 4000:4000 todo-app
<img width="1920" height="1028" alt="Screenshot 2026-01-12 141450" src="https://github.com/user-attachments/assets/2398b810-2f93-4257-8d63-d019b962bd40" />


### Step 5: Create CI Pipeline Using GitHub Actions

A GitHub Actions workflow was created to:

Build Docker image

Login to private Docker registry

Push image on every push to main

Workflow file:

.github/workflows/docker-ci.yml


**Pipeline steps:**

Checkout code

Login to Docker Hub using secrets

Build image

Push image


<img width="1920" height="894" alt="image" src="https://github.com/user-attachments/assets/898ae213-1bd3-447b-9089-de714e083f4f" />
<img width="1920" height="1020" alt="Screenshot 2026-01-12 142514" src="https://github.com/user-attachments/assets/7502cc74-206e-4466-ab33-e539a934cdd8" />



## Part 2: Configuration Management with Ansible (30 Points)
**Objective**

Provision a Linux VM and configure it using Ansible from the local machine.

### Step 1: Create Linux VM

A Linux virtual machine was created using AWS.
<img width="1920" height="239" alt="image" src="https://github.com/user-attachments/assets/edfd45c3-b443-4b3c-98a6-b2e04186353b" />

<img width="1920" height="257" alt="image" src="https://github.com/user-attachments/assets/3ee5d9eb-0b70-4baa-a033-f104b79e4664" />

VM running (OS info or terminal)

### Step 2: Install Ansible on Local Machine

Ansible was installed on the local machine.

sudo apt install ansible -y


### Step 3: Configure Inventory File

An inventory file was created pointing to the VM IP.

[vm]
192.168.x.x ansible_user=merna ssh=mykeypath


### Step 4: Ansible Playbook to Install Docker

An Ansible playbook was created to:

Update system

Install Docker

Enable and start Docker service

ansible-playbook install-docker.yml


<img width="960" height="1020" alt="Screenshot 2026-01-12 150624" src="https://github.com/user-attachments/assets/7625a940-14e3-4d46-9397-072f81cd14aa" />

Playbook file
Successful playbook execution


## Part 3: Application Deployment & Auto Update (40 Points)
Objective

Run the application using Docker Compose and enable automatic updates when the image changes.

### Step 1: Docker Compose Setup

A docker-compose.yml file was created to run the application.

**Key features:**

Uses Docker image from registry

Maps ports

Uses .env file

Configured health check

healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:4000"]
  interval: 30s
  retries: 3

### Step 2: Run Application on VM

The application was successfully started on the VM.

docker compose up -d
<img width="960" height="1020" alt="Screenshot 2026-01-12 151518" src="https://github.com/user-attachments/assets/456025fb-fd74-4b94-993a-bed2c571ec38" />

## Part 4: Bonus – Kubernetes & GitOps with ArgoCD (50 Points)
**Objective**

Replace Docker Compose with Kubernetes and use ArgoCD for Continuous Deployment.

### Step 1: Setup Kubernetes Cluster

Minikube was used to create a Kubernetes cluster.

minikube start

### Step 2: Kubernetes Manifests

Created Kubernetes manifests:

Deployment

Service (NodePort)
<img width="960" height="1020" alt="Screenshot 2026-01-12 190523" src="https://github.com/user-attachments/assets/f9f21b63-ac4d-4d9f-8145-b4ef259a2c29" />
<img width="960" height="1020" alt="Screenshot 2026-01-12 191157" src="https://github.com/user-attachments/assets/bf7b8036-9dd3-46b6-95cb-a0ef7fcf9a90" />


### Step 3: Install ArgoCD

ArgoCD was installed in the cluster.

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml


### Step 4: ArgoCD Application (GitOps)

An ArgoCD Application was created pointing to the GitHub repository containing Kubernetes manifests.

Repo URL

Path to manifests

Target namespace

Auto-sync enabled
<img width="960" height="1020" alt="Screenshot 2026-01-12 212947" src="https://github.com/user-attachments/assets/cf1a193e-0547-4608-9dd6-ae108ddac980" />

## Final Result

CI pipeline builds and pushes images automatically

Infrastructure configured using Ansible

Application auto-updates on image changes

Kubernetes deployment managed via GitOps using ArgoCD



