# Docker & Containerization Study Notes

## What are Containers?

Containers are lightweight portable units for applications and they bond applications with all its dependencies so the app runs consistent across different environments.

For example if you have an app and want to run all parts of that app containers will include the code, the run time and anything needed this includes dependencies that and application needs to run.

Because they are isolated it runs the same on any environment and can be ran anywhere whether its a laptop or an virtual environment the application will run the same in that container.

## 🐳 Docker Architecture

![Docker Architecture](https://github.com/user-attachments/assets/bb5d1b9d-87a7-49a8-aa30-3c3926dc4dfb)

### Architecture Components:

**Infrastructure** - represents the physical or virtual hardware where everything runs

**Host Operating System** - this is the OS that the infrastructure uses

**Docker Engine** - makes containerisation possible, it provides the environment to build, run and manage containers without docker your containers wont run

**Docker Containers** - each container holds and application and its dependencies

This isolation ensures each app runs consistently on different environments as they wont be able to interact with each other they are like shipping containers. In the diagram there is 3 containers on one engine they all share the same engine but are isolated in each container this makes them lightweight and efficient because they share the engine and os system as the containers sit above them.

## Benefits of Containers

### Isolation
Each container is isolated and have their own environment and this helps prevent conflict and ensures that applications run smoothly without interfering with each other.

**Example:**
If app C ran on python2.7 and app B ran on python 3.8 isolation helps make sures that these 2 applications dont clash because of different versions.

This is where isolation comes in handy because containers provide a consistent environment for applications to run this ensures an application will behave the same way regardless of where its deployed this eliminates issues such as an application working on a developer computer and for another environment due to missing dependencies or different configurations.

An example of this if a dev has a windows laptop and the app runs fine and then is moved over to a dev with a macOS the app might not work because of the different dependencies and environments.

### Efficiency
Containers are efficient because of how they are ran, they sit on the dockers engine which shares the whole operating system / kernel making them more resource friendly than virtual machines this reduces overhead and allows many containers to run on 1 hardware this makes the containers faster to start up and resource efficient.

## What is Docker?

Docker is an open platform used for developing, shipping and running applications in containers and is one of the most popular for it. It simplifies the process of managing containers making it easier to build, deploy and run apps.

### Docker Key Components:

**Docker Engine** - this is the component that runs and manages the containers and is the core of docker its like a car engine its what powers the whole thing the docker engine is responsible for creating and running containers based on the instructions in the docker file and images

**DockerHub** - docker hub is a repo where you can find a share container images its like the app store for docker images you can pull official images, community images and share your own images with others

**Docker Compose** - a tool for defining and running multi container docker applications

## Images and Containers

### What are Images?
Images are templates for creating containers and image is like a snap shot of an application at a certain point of time they are immutable meaning they dont change once they have been created to change them you have to create the image again immutability ensures apps run consistently no matter where its deployed.

### What are Containers?
Containers are running instance of images so the images are the snapshots of an app containers are what run these images containers are what you interact with they can start stop or be edited.

### How are Images Created?
Theres a thing called docker file and its used to build docker images, it contains a series of instructions that are used to build a docker image.

![Docker Image Creation](https://github.com/user-attachments/assets/5060ef9a-bb09-427d-9fec-41d0f3f534eb)

## Importance in Modern Development

**Simplified Deployment** - Docker simplified deployment by eliminating the trouble of running applications across different environments and has allowed these applications to run consistently within its container.

**Improved Efficiency** - Docker improved efficiency because virtual machines are resource heavy and slow to start up however docker is lightweight as it shares the systems kernel which allows them to start up quicker and use less resource developers can start up containers quickly and companies prefer this because if the efficiency.

**Better Collaboration** - Docker bettered collaboration because it made it easy to share environments and applications with team members instead of setting up a complex environment on each machine you can just share a docker file and this makes sure everything is consistent and the same on everyone machine makes it easy for new developers to onboard as it saves time of setting up environments and docker integrates with cicd automation well.

## 🔥 FAMOUS Interview Question: VMs vs. Containers

### 🔹 Virtual Machines (VMs):
- Run a full guest operating system on top of a hypervisor
- Each VM is isolated and includes its own OS, binaries, and libraries
- Resource-heavy – uses more CPU, memory, and storage
- Slow startup – takes minutes to boot
- Strong isolation, ideal for running different OS types or when full OS-level separation is needed
- Less portable, often tied to specific hypervisors

### 🔹 Containers:
- Run on the Docker engine which sits on top of the host OS
- Share the host OS kernel, no need for a guest OS
- Lightweight and efficient, containing only the app and its dependencies
- Fast startup – takes seconds
- Process-level isolation – sufficient for most use cases
- Highly portable, thanks to Docker images, ideal for cloud-native development

![VMs vs Containers](https://github.com/user-attachments/assets/f76f11fb-d017-4957-9b54-412aca30f36e)

### 🔑 Key Differences:

| Feature | Virtual Machines | Containers |
|---------|------------------|------------|
| Startup Time | Minutes | Seconds |
| Resource Usage | High (full OS per VM) | Low (share host OS) |
| Isolation | Strong (full OS isolation) | Process-level (shares host kernel) |
| Portability | Less portable | Very portable (Docker images) |

![Comparison Diagram](https://github.com/user-attachments/assets/9ac27621-8492-4e7f-b7f7-ac8b3951e26e)

### 💡 Why It Matters:
- **Use VMs** when you need strong isolation or to run different OS types
- **Use containers** when you need speed, scalability, and efficiency for modern apps

## Dockerfile

### 🔹 What is a Dockerfile?
A Dockerfile is a text file with step-by-step instructions to build a Docker image. It's like a recipe for creating a consistent, repeatable containerized environment. Each instruction in the Dockerfile creates a layer in the image, which helps with caching and optimization.

### 🔹 Why is it Important?
- Enables repeatable builds for consistent development and deployment
- Acts as the foundation for creating Docker images and running containers

### 🔹 Key Dockerfile Instructions

**FROM** - Sets the base image (e.g., node:14, python:3.10) Every image builds on top of another image.

**WORKDIR** - Sets the working directory inside the container for the following instructions. Example: `WORKDIR /app`

**COPY** - Copies files from your local machine into the container. Example: `COPY package*.json ./`

**RUN** - Executes commands in the container while building the image. Common for installing dependencies. Example: `RUN npm install`

**EXPOSE** (optional) - Informs Docker that the container will use a specific port (e.g., `EXPOSE 3000`).

**CMD** - Sets the default command to run when the container starts.

### Example Dockerfile Breakdown (Node.js App)

```dockerfile
FROM node:14
# Use the official Node.js v14 image as the base.

WORKDIR /app
# Set /app as the working directory inside the container.

COPY package*.json ./
# Copy package.json and package-lock.json into the container.

RUN npm install
# Install Node.js dependencies inside the container.

COPY . .
# Copy the rest of the application code into the container.

EXPOSE 3000
# Let Docker know the app runs on port 3000.

CMD ["node", "index.js"]
# Start the application by running node index.js.
```

![Dockerfile Example](https://github.com/user-attachments/assets/dcdcbfad-9925-4318-bc85-e18de367a37b)

## Docker Networking

Docker provides several default network options that you can use to link containers:

**Bridge Network** - default network mode for containers on same machine containers on a bridge can communicate with each other using their own ip addresses isolated from host machine network providing extra security.

**Host Network** - host mode a container uses the host machines network directly without any isolation its like if the container is plugged directly into your home network useful for applications that need to crash with the host system.

**None Type** - this gives a container no network interface like a room without windows or doors and is completely isolated used when you want to ensure a container has no network access useful for security scenarios.

### Importance in DevOps
In DevOps, Docker networking is important because it helps microservices work together. Each part of an app can run in its own container, and Docker makes sure they can talk to each other safely and smoothly. You can choose different network types like bridge, host, or none, depending on what you need. It also works no matter where the containers are running. Plus, Docker networking is easy to scale, so as your app grows, your services can grow too.

## Docker Compose

### What is Docker Compose?
Docker compose helps you manage and run multiple containers together by keeping them in a single yml file so instead of manually starting and stopping singular containers you and run multiple imagine if your app had a data base, webserver etc in different containers docker compose allows you to run them all together.

### 🔑 Key Features of Docker Compose

#### 📄 `docker-compose.yml` File
- Defines all the services your application needs
- Acts as a blueprint for your environment
- Specifies:
  - Docker images
  - Ports to expose
  - Volumes
  - Dependencies between containers
  - Environment variables

#### 🧪 Commands
Manage your entire stack with simple CLI commands:
- `docker-compose up` → Starts all containers
- `docker-compose down` → Stops and removes containers, networks, and volumes
- `docker-compose ps` → Lists running services
- `docker-compose logs` → Shows logs for services

No need to handle containers individually.

#### 🌐 Networking
- Automatically creates a shared network for your services
- Containers can communicate using service names (e.g., db, web)
- No need for manual network setup
- Ensures seamless communication between containers

### 🚀 Why Docker Compose is Important in DevOps

#### 🔧 1. Simplifies Development & Testing
- Quickly spin up full environments with all required services (e.g. MySQL, Nginx, Redis)
- No need to manually configure each service
- Speeds up setup → more time writing code, less time managing infrastructure
- Useful for replicating production environments locally for testing

#### ✅ 2. Ensures Consistency Across Environments
- Solves the "it works on my machine" problem
- Everyone uses the same environment setup:
  - Local development
  - CI/CD pipelines
  - Production
- Defined in a single `docker-compose.yml` file → fewer bugs and environment-related errors

#### 🤝 3. Enhances Teamwork & Collaboration
- Team members work in identical environments
- Environment setup can be version controlled alongside code
- New developers can:
  - Clone the repo
  - Run `docker-compose up`
  - Instantly get the full working environment
- Makes onboarding faster and documentation simpler

### 🧠 Summary
Docker Compose is essential in DevOps because it:
- ✅ Simplifies environment setup
- ✅ Ensures consistency across development, testing, and production
- ✅ Improves collaboration and onboarding

## Docker Registries

### What is a Docker Registry?
A docker registry is a system for storing and sharing docker images its like an online library that stores your images for when ever you need them.

### Key Features:
**Public Registries** - like docker hub is open to everyone where you can share your images and use community provided images

**Private Registries** - like AWS ECR which are secure and only I have access to crucial for dealing with sensitive applications

### Importance of Docker Registries in DevOps:

**Streamlined Deployment** - They streamline the deployment process once they are stored in the registry they can be easily accessed and deployed across different environment and is more reliable to roll out new features / updates

**Enhanced Collaboration** - When images are stored in a registry the team has access to the same image making development easier and making work faster

**Ensures Consistency** - By storing you image in a registry it makes sure that same image is being used in development testing and production eliminating it doesnt work on my machine problem
j
