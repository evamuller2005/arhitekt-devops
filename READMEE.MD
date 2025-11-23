# Arhitekt Project 

### Overview

The Arhitekt Project is a simplified web application designed for browsing architectural projects and viewing detailed information about each project. This repository contains information on how to run the app locally, as well as how to provision a VM using Vagrant.

---

### Key Features

- Browse projects: A homepage displaying all published architectural projects
- Project details: Individual project pages with descriptions.

---

### Tech Stack

- HTML
- CSS
- JavaScript
- C# / .NET 

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

`wget https://packages.microsoft.com/config/ubuntu/22.04packages-microsoft-prod.deb -O packages-microsoft-prod.deb`
`sudo dpkg -i packages-microsoft-prod.deb`
`sudo apt update`

##### 7. Install .NET 8 SDK

`sudo apt install -y dotnet-sdk-8.0`

##### 8. Go to your backend project folder (THIS is the correct one)

`cd Arhitekt/`

##### 9. Run the application

`dotnet build`   
`dotnet run`   

---

### System Requirements for Vagrant

##### Host machine requirements

- Linux (Ubuntu recommended)
- VirtualBox
- Vagrant
- Git

#### Installed automatically inside the VM

- .NET SDK / Runtime
- Nginx
- Required system packages
- Systemd service (arhitekt-backend.service)

---

### Vagrant

#### 1. Install required packages:

`sudo apt update`

`sudo apt install virtualbox virtualbox-dkms linux-headers-generic-hwe-22.04`

`wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list sudo apt update && sudo apt install vagrant`

`sudo apt install git -y`

#### 2. Clone the repo, and enter the vagrant folder:

`git clone https://github.com/evamuller2005/arhitekt-devops.git`

#### 3. run the vagrant command from varant directory:

`cd fitness-project/infra/vagrant`
`vagrant up`

---

Link to the deployment video: 