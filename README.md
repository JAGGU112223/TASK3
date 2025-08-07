Task 3 - Infrastructure as Code (IaC) with Terraform and Docker
📌 Objective
Provision a local Docker container using Terraform to understand Infrastructure as Code (IaC) concepts. This task automates container deployment without using manual Docker commands.

🛠 Tools Used
Terraform – For infrastructure automation
Docker – To run the container locally
EC2 (Amazon Linux) – As the base machine where everything is installed
📁 Files in this Repository
File	Description
main.tf	Terraform configuration file
README.md	Documentation for the task
execution_log.txt (optional)	Terraform output from apply/destroy
🔧 Setup Steps (Executed on Fresh EC2)
Installed Docker

sudo yum install -y docker
sudo systemctl start docker
sudo usermod -aG docker ec2-user
Installed Terraform

sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
Wrote Terraform configuration (main.tf) using Docker provider.

📄 main.tf Overview
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.20.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx" {
  name  = "nginx_container"
  image = docker_image.nginx.latest
  ports {
    internal = 80
    external = 8080
  }
}
