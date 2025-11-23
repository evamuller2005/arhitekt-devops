# Arhitekt Project Overview

**Purpose:**
The Arhitekt Project is a simplified web application designed for browsing architectural projects and viewing detailed information about each project. This repository contains the automation required to deploy the Arhitekt application using Vagrant, Ansible.

The goal is to offer a fully reproducible VM environment that deploys the application with a single command.

---

#### Key Features

- Browse projects: A homepage displaying all published architectural projects
- Project details: Individual project pages with descriptions, images, categories, and metadata
- Simple and clean UI: Lightweight frontend for fast browsing

---

## Tech Stack

- HTML
- CSS
- JavaScript
- C# / .NET Web API

---

## System Requirements

#### Host machine requirements

- Linux (Ubuntu recommended)
- VirtualBox
- Vagrant
- Git

#### Installed automatically inside the VM

- .NET SDK / Runtime
- Nginx
- Required system packages
- Systemd service (arhitekt-backend.service)

## Vagrant 

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

Link to the deployment video: 