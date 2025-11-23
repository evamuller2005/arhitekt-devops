# Arhitekt Project 

### Overview

The Arhitekt Project is a simplified web application for browsing architectural projects and viewing detailed information about each one.
It is built with C#/.NET, Razor views, and a simple frontend.
This repository also includes instructions for running the app locally and provisioning it via Vagrant + Ansible on a virtual machine.

---

### Key Features

- Browse projects: A homepage displaying all architectural projects
- Project details: Individual pages showing name, description, images, and metadata
- Database seeding: Projects are automatically inserted on first run
- Simple UI: Lightweight and fast Razor-based frontend

---

### Tech Stack

##### Frontend:

- HTML
- CSS
- JavaScript
- Razor Pages

##### Backend:

- C# / .NET 8
- Entity Framework Core (Database auto-created via EnsureCreated)
- Redis (caching)
- MSSQL Server (running in Docker)

##### Infrastructure:

- Vagrant
- Ansible
- Ubuntu Linux
- Nginx (inside VM, for production)
- Systemd service for backend

---

### Run Locally

##### 1. Clone the repository

`git clone https://github.com/evamuller2005/arhitekt-devops.git`   

`cd arhitekt-devops`

##### 2. Update system

`sudo apt update`

##### 3. Install Docker (for MSSQL + Redis)

`sudo apt install -y docker.io`   
`sudo systemctl enable docker`   
`sudo systemctl start docker`   

##### 4. Run SQL Server in Docker

`sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Arhitekt2025" -e "MSSQL_PID=Developer" -p 1433:1433 --name arhitekt-sql -d mcr.microsoft.com/mssql/server:2022-latest`

##### 5. Run Redis in Docker

`sudo docker run --name arhitekt-redis -p 6379:6379 -d redis:latest`

##### 6. Install Microsoft package feed for .NET 8

`wget wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb`
`sudo dpkg -i packages-microsoft-prod.deb`
`sudo apt update`

##### 7. Install .NET 8 SDK

`sudo apt install -y dotnet-sdk-8.0`

##### 8. Navigate to the project folder

`cd Arhitekt/`

##### 9. Run the application

`dotnet build`   
`dotnet run`   

##### App will start on http://localhost:5059

---

### System Requirements for Vagrant

##### Host machine requirements

- Linux (Ubuntu recommended)
- VirtualBox
- Vagrant
- Git

##### Installed automatically inside the VM

- .NET SDK / Runtime
- Nginx reverse proxy
- Required system packages
- Systemd service (arhitekt-backend.service)

---

### Vagrant

##### 1. Install required packages:

`sudo apt update`    
`sudo apt install virtualbox virtualbox-dkms linux-headers-generic-hwe-22.04`    
`wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg`   
`echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list`   
`sudo apt update && sudo apt install vagrant`
`sudo apt install git -y`  

##### 2. Clone the repository:

`git clone https://github.com/evamuller2005/arhitekt-devops.git`

##### 3. Run Vagrant from the correct directory:

`cd fitness-project/infra/vagrant`  
`vagrant up`

---

## Deployment Video Explanation

The video shows the full deployment process of the Arhitekt application using Vagrant on my assigned DevOps VM. From my local machine (macOS) I connect to the DevOps VM via SSH, and inside this remote environment I use Vagrant to create a nested VirtualBox VM, which is then fully provisioned using Vagrant + Ansible (installing .NET, configuring Nginx, deploying the published app, and creating a systemd service).

Additionally, on the DevOps VM itself, I configured Nginx as a reverse proxy that exposes the application publicly through the university domain https://devops-vm-30.lrk.si/
. This reverse proxy listens on port 443 and forwards incoming HTTPS traffic to the nested VM where the Arhitekt application is running internally, allowing the app to be securely accessible from the internet without exposing VirtualBox ports.

The video demonstrates the entire automated provisioning workflow, the service starting successfully, and how the deployed application becomes reachable through the Nginx reverse-proxy domain.


- an SSH tunnel from my local machine (macOS)
- into the DevOps environment
- where a nested VirtualBox VM is created
- and fully provisioned using Vagrant + Ansible



Link to the deployment video: 