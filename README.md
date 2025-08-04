Docker Notes

## what are containers?
containers are lightweght portable portable units for applications 
and they bond appl;icationbs with all its dependencies so the app runs consistant across diffferent environemnts 

for example if you ahve an app and want to run all parts of that app
conatiners will include the code, the run time and anything needed this includes dependencies that and application needs to run

because they are isolated it runs the same on any environment and can be ran anywhere 
wether itsa loptop or an virtual environmewnt the application will run the same in that contaner

🐳 Docker Architecture – Simplified Notes
Infrastructure (Bottom Layer)

This is your host machine (e.g., your laptop or server).

Host Operating System

The OS installed on your machine (e.g., Windows, macOS, or Linux).

Docker Engine

A lightweight container runtime that manages and runs containers.

Sits on top of the host OS.

Containers (3 in this case)

Each container includes:

The application

Its binary (compiled code)

All required libraries/dependencies

Each container is isolated, but they share the same Docker Engine.

diagram
<img width="693" height="343" alt="image" src="https://github.com/user-attachments/assets/bb5d1b9d-87a7-49a8-aa30-3c3926dc4dfb" />

infrastructure - represents the physical or virtual hardware where everything runs
host operating system - this is the OS that the infrastructure uses 
docker engine - makes contanerisation possible, it provides the environment to build, run and manage containers
without docker your containers wont run
docker containers - each container holds ands application and its dependencies 

this isolation ensures each app runs consistantly on different environments as theywont be able to interact with each other
they are like shipping containers 
in the diagram there is 3 containers on one engine they all share the same engine but are isolated in each container
this makes them lightweight and effeciant because they sharee the engine and os system as  the containers sit above them 

## benefits of containers

isolation - each container is isolated and have their own enivronment and this helps prevent conflict and ensures that applications run smoothly without interfearing with each other

example:
if app C ran on python2.7 and app B ran on python 3.8 isolation helps make sures that these 2 applications dont clash becaiuse of different versions 

this is where isolation comes in handly bacause containers provide a consistant environment for applications to run 
this ensures an application will behave the same way regardless of where its deployed 
this eleminates issues such as an application working on a developer computer and for another environment due to missing dpendencies or different configurations 

an example of this if a dev has a windows laptop and the app runs fine and then is moved over to a dev with a macOS the app might not work because of the different dependencies and envronments

containers are efficient because of how they are ran, they sit on the dsockers engine which shares the whole operating system / kernel making them more recourse friendly than virtual machines
thios reduces overhead and allows many containers to run on 1 hard ware
this makes the containers faster to start up and resource efficient

## what is docker?
docker is an open platform used for developing, shipping and running applications in containers and is one of the most popular for it 
It simplifies the proces of managing containers making it easier to build,deploy and run apps

docker has several key components:
Docker engine - this is the component that runs and manages the containers and is the core of docker its like a car engine its what powers the whole thing
the docker engineine is responsible for creating and running containerzs based ont he instructions in the docker file and images

dockerhub- docker hub is a repo where you can find a share container images its like the app store for docker images  you can pull official images,community images and share your own ikmages with others
docker compose - a tool for defining and running multi container docker applications 

## Images and Containers
what are images?
images are templates for creating containers and image is like a snap shot of an application at a certain point of time 
they are immutable meaning they dont change once they have been created to change them you have to create the image again 
immutability ensures apps run consistantky no matter where its deployed

what are containers?
containers are running instance of images so the images are the snapshots of an app containers are what run these images
containers are what you interact with they can start stop or be edited 

how are images created?
theres a thing called docker file and its used to build docker images, it containes a series of instructions that are used to build a docker image 

<img width="1104" height="710" alt="image" src="https://github.com/user-attachments/assets/5060ef9a-bb09-427d-9fec-41d0f3f534eb" />

## Importance in Modern Development
docker simplified deployment by eliminating the trouble of running applications accross different environments and has allowed these applications to run consitantky within its container 
docker improved effeciency becasue virtual machines are resouce heavy and slowm to start up however docker is lightweight as it shares the systems kernal whicha llows them to start up quicker and use less resource 
developers can start up containers quickly and companies prefer this because oif the efficiendy
docker bettered collaberation because it made it easy tio share environmentrs and apllications with team members 
instead of setting up a complex environment one ach machine you can just share a docker file and this makes sure everything is consistent and the same on everyone machine 
makes it easy for new developers to onboard as it saves time of settin  g up environments and docker intergrates with cicd automation well 

## FAMOUS Interview Question: VMs vs. Containers
🐳 Containers vs Virtual Machines – Summary
🔹 Virtual Machines (VMs):

Run a full guest operating system on top of a hypervisor.

Each VM is isolated and includes its own OS, binaries, and libraries.

Resource-heavy – uses more CPU, memory, and storage.

Slow startup – takes minutes to boot.

Strong isolation, ideal for running different OS types or when full OS-level separation is needed.

Less portable, often tied to specific hypervisors.

🔹 Containers:

Run on the Docker engine which sits on top of the host OS.

Share the host OS kernel, no need for a guest OS.

Lightweight and efficient, containing only the app and its dependencies.

Fast startup – takes seconds.

Process-level isolation – sufficient for most use cases.

Highly portable, thanks to Docker images, ideal for cloud-native development.
<img width="747" height="363" alt="image" src="https://github.com/user-attachments/assets/f76f11fb-d017-4957-9b54-412aca30f36e" />

🔑 Key Differences:
Feature	Virtual Machines	Containers
Startup Time	Minutes	Seconds
Resource Usage	High (full OS per VM)	Low (share host OS)
Isolation	Strong (full OS isolation)	Process-level (shares host kernel)
Portability	Less portable	Very portable (Docker images)
<img width="776" height="419" alt="image" src="https://github.com/user-attachments/assets/9ac27621-8492-4e7f-b7f7-ac8b3951e26e" />

💡 Why It Matters:
Use VMs when you need strong isolation or to run different OS types.

Use containers when you need speed, scalability, and efficiency for modern apps.
🔹 What is a Dockerfile?
A Dockerfile is a text file with step-by-step instructions to build a Docker image.

It’s like a recipe for creating a consistent, repeatable containerized environment.

Each instruction in the Dockerfile creates a layer in the image, which helps with caching and optimization.

🔹 Why is it Important?
Enables repeatable builds for consistent development and deployment.

Acts as the foundation for creating Docker images and running containers.

🔹 Key Dockerfile Instructions
FROM

Sets the base image (e.g., node:14, python:3.10)

Every image builds on top of another image.

WORKDIR

Sets the working directory inside the container for the following instructions.

Example: WORKDIR /app

COPY

Copies files from your local machine into the container.

Example: COPY package*.json ./

RUN

Executes commands in the container while building the image.

Common for installing dependencies.

Example: RUN npm install

EXPOSE (optional)

Informs Docker that the container will use a specific port (e.g., EXPOSE 3000).

CMD

Sets the default command to run when the container starts.

example  Dockerfile Breakdown (Node.js App)
FROM node:14
➤ Use the official Node.js v14 image as the base.

WORKDIR /app
➤ Set /app as the working directory inside the container.

COPY package*.json ./
➤ Copy package.json and package-lock.json into the container.

RUN npm install
➤ Install Node.js dependencies inside the container.

COPY . . (shown as just COPY in the image, but should be this)
➤ Copy the rest of the application code into the container.

EXPOSE 3000
➤ Let Docker know the app runs on port 3000.

CMD ["node", "index.js"]
➤ Start the application by running node index.js.
<img width="465" height="285" alt="image" src="https://github.com/user-attachments/assets/dcdcbfad-9925-4318-bc85-e18de367a37b" />






















































































































































































