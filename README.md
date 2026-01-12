
# todo-app
=======
# Todos-nodejs
=======


## Documentation
This project demonstrates a complete DevOps workflow including CI, configuration management, containerization, auto-deployment, and GitOps using ArgoCD.

🔹 Part 1: CI Pipeline & Dockerization (30 Points)
Objective

Containerize the Todo Node.js application and build a CI pipeline that pushes the Docker image to a private registry.

Step 1: Clone the Application Repository

The application repository was cloned from GitHub:

git clone https://github.com/Ankit6098/Todo-List-nodejs.git

cd Todo-List-nodejs


Step 2: Configure MongoDB Database

A personal MongoDB database was created and configured in the .env file.

Updated MONGO_URI

Updated application port if needed

Example:

MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/todo
PORT=4000


Step 3: Dockerize the Application

A Dockerfile was created to containerize the Node.js application.

Key points:

Used official Node.js base image

Installed dependencies

Exposed application port

Used npm start as entrypoint

FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 4000
CMD ["npm", "start"]



Step 4: Build and Test Docker Image Locally

The Docker image was built and tested locally to ensure it works correctly.

docker build -t todo-app .
docker run -p 4000:4000 todo-app


Step 5: Create CI Pipeline Using GitHub Actions

A GitHub Actions workflow was created to:

-Build Docker image
-Login to private Docker registry
-Push image on every push to main

Workflow file:

.github/workflows/docker-ci.yml


Pipeline steps:

-Checkout code
-Login to Docker Hub using secrets
-Build image
-Push image


<img width="1920" height="894" alt="image" src="https://github.com/user-attachments/assets/898ae213-1bd3-447b-9089-de714e083f4f" />


