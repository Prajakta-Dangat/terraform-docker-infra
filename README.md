# Terraform Docker Infrastructure

## 📌 Project Overview

This project demonstrates **Infrastructure as Code (IaC)** using **Terraform** to provision and manage a local Docker container.

Terraform is used to:

- Pull an NGINX Docker image
- Create an NGINX Docker container
- Configure port mapping
- Preview infrastructure changes using `terraform plan`
- Provision infrastructure using `terraform apply`
- Manage resources using Terraform State
- Destroy infrastructure using `terraform destroy`

---

## 🎯 Objective

The main objective of this project is to understand how **Terraform can be used to manage Docker infrastructure as code** instead of manually creating Docker containers using Docker CLI commands.

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Terraform | Infrastructure as Code |
| Docker | Containerization |
| NGINX | Web Server |
| PowerShell | Command Line |
| Git | Version Control |
| GitHub | Source Code Management |

---

## 🏗️ Architecture

```text
                    Terraform
                        |
                        |
                    main.tf
                        |
                        ▼
                Docker Provider
                        |
                        ▼
                  Docker Engine
                        |
             ┌──────────┴──────────┐
             ▼                     ▼
        NGINX Image          NGINX Container
                                   |
                                   |
                              Port 8081
                                   |
                                   ▼
                         http://localhost:8081
```

---

## 📂 Project Structure

```text
terraform-docker-infrastructure/
│
├── main.tf
├── .gitignore
├── .terraform.lock.hcl
└── README.md
```

### Files Description

- `main.tf` - Terraform configuration for Docker image and container.
- `.gitignore` - Prevents Terraform state and temporary files from being uploaded.
- `.terraform.lock.hcl` - Locks the Terraform provider version.
- `README.md` - Project documentation.

---

# 🚀 Prerequisites

Before running this project, make sure the following are installed:

### Terraform

Check Terraform:

```powershell
terraform version
```

### Docker Desktop

Check Docker:

```powershell
docker --version
```

Check whether Docker is running:

```powershell
docker ps
```

Make sure **Docker Desktop is running** before executing Terraform commands.

---

# ⚙️ Terraform Configuration

The project uses the Docker provider.

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "4.6.0"
    }
  }
}

provider "docker" {}
```

---

# 🐳 Docker Image

Terraform pulls the NGINX Docker image:

```hcl
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

This allows Terraform to manage the NGINX Docker image.

---

# 📦 Docker Container

Terraform creates an NGINX container:

```hcl
resource "docker_container" "nginx" {
  name  = "terraform-nginx"
  image = docker_image.nginx.image_id

  ports {
    internal = 80
    external = 80
  }
}
```

### Port Mapping

```text
Host Port 80  →  Container Port 80
```

The NGINX application can be accessed using:

```text
http://localhost:8081
```

---

# 🔄 Terraform Workflow

The project follows the standard Terraform workflow:

```text
Write Terraform Code
        ↓
terraform init
        ↓
terraform fmt
        ↓
terraform validate
        ↓
terraform plan
        ↓
terraform apply
        ↓
Verify Docker Container
        ↓
Terraform State
        ↓
terraform destroy
```

---

# 🧑‍💻 How to Run the Project

## Step 1: Clone the Repository

```bash
git clone https://github.com/Prajakta-Dangat/terraform-docker-infrastructure.git
```

Go inside the project:

```bash
cd terraform-docker-infrastructure
```

---

## Step 2: Initialize Terraform

Run:

```bash
terraform init
```

This downloads and initializes the required Docker provider.

Expected output:

```text
Terraform has been successfully initialized!
```

---

## Step 3: Format Terraform Code

Run:

```bash
terraform fmt
```

This formats the Terraform configuration according to Terraform standards.

---

## Step 4: Validate Terraform Configuration

Run:

```bash
terraform validate
```

Expected output:

```text
Success! The configuration is valid.
```

---

## Step 5: Create Terraform Plan

Run:

```bash
terraform plan
```

This command shows what Terraform is going to create without actually creating the infrastructure.

Expected result:

```text
Plan: 2 to add, 0 to change, 0 to destroy.
```

Resources:

```text
docker_image.nginx
docker_container.nginx
```

---

## Step 6: Apply Infrastructure

Run:

```bash
terraform apply
```

Terraform will ask for confirmation.

Enter:

```text
yes
```

Terraform will:

1. Pull the NGINX image.
2. Create the Docker container.
3. Configure port mapping.
4. Store the infrastructure information in Terraform state.

Expected output:

```text
Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```

---

# 🔍 Verify Docker Container

Check running containers:

```bash
docker ps
```

The container should be:

```text
terraform-nginx
```

You can also check all containers:

```bash
docker ps -a
```

---

# 🌐 Access NGINX

Open a web browser and visit:

```text
http://localhost:80
```

You should see the NGINX welcome page:

```text
Welcome to nginx!
```

---

# 📋 Terraform State

Terraform maintains information about the infrastructure in its state file.

### List Terraform-managed resources

```bash
terraform state list
```

Expected output:

```text
docker_container.nginx
docker_image.nginx
```

### Show container state

```bash
terraform state show docker_container.nginx
```

### Show complete Terraform state

```bash
terraform show
```

---

# 🗑️ Destroy Infrastructure

When the project is completed, destroy the infrastructure using:

```bash
terraform destroy
```

Enter:

```text
yes
```

Terraform will remove the resources created by this project.

Expected output:

```text
Destroy complete! Resources: 2 destroyed.
```

---

# 🔐 Git Ignore

Terraform state files and temporary files should not be committed to GitHub.

The `.gitignore` file excludes:

```text
.terraform/
*.tfstate
*.tfstate.*
*.tfvars
crash.log
```

The following file should be committed:

```text
.terraform.lock.hcl
```

---

# 📚 Important Terraform Commands

| Command | Description |
|---|---|
| `terraform init` | Initialize Terraform and download providers |
| `terraform fmt` | Format Terraform code |
| `terraform validate` | Validate Terraform configuration |
| `terraform plan` | Preview infrastructure changes |
| `terraform apply` | Create or update infrastructure |
| `terraform state list` | List Terraform-managed resources |
| `terraform state show` | Display details of a resource |
| `terraform show` | Display Terraform state |
| `terraform destroy` | Destroy Terraform-managed infrastructure |

---

# 💡 Key Concepts Learned

Through this project, I learned:

- Infrastructure as Code (IaC)
- Terraform providers
- Terraform resources
- Docker provider
- Docker images
- Docker containers
- Port mapping
- Terraform initialization
- Terraform plan
- Terraform apply
- Terraform state management
- Terraform destroy
- Managing Docker infrastructure using Terraform

---

# 🎯 Project Outcome

Successfully provisioned and managed a local **NGINX Docker container using Terraform**.

The complete lifecycle was managed using:

```text
terraform init
        ↓
terraform plan
        ↓
terraform apply
        ↓
terraform state
        ↓
terraform destroy
```

This project demonstrates the practical implementation of **Infrastructure as Code (IaC)** using **Terraform and Docker**.

---

# 👩‍💻 Author

## Prajakta Pramod Dangat

**BTech E&TC Engineering | Cloud & DevOps Enthusiast**

### GitHub

https://github.com/Prajakta-Dangat

### LinkedIn

https://linkedin.com/in/prajakta-d-619086315
