# Terraform 2-Tier Web App on AWS

This project demonstrates how I deployed a 2-tier architecture on AWS using **Terraform**, including a VPC, public and private subnets, internet gateway, security group, and an EC2 instance. It also documents the tools used, step-by-step commands, screenshots, challenges encountered, and lessons learned.

---

## 📁 Project Structure

The project is organized using separate Terraform configuration files for modularity and clarity.

![Initial Terraform project structure](screenshots/01-project-folder-structure.png)

---

## 🛠️ Tools Used

- **Terraform**
- **AWS CLI**
- **Visual Studio Code** with **WSL (Ubuntu)** on Windows
- **Git & GitHub**

---

## 🚀 Step-by-Step Guide

### 1. Installed Visual Studio Code and Launched WSL

I installed VS Code on Windows and set up **WSL (Ubuntu)** for Linux-based development. This allowed me to run Linux commands and use Terraform efficiently.

![VS Code Installed](screenshots/01-vscode-installed.png)

![WSL Ubuntu inside VS Code](screenshots/02-ubuntu-terminal-in-vscode.png)

---

### 2. Created Project Folder and Terraform Files

Inside the Linux terminal (WSL), I created a project folder and added the following files:

```bash
mkdir terraform-aws-project
cd terraform-aws-project
touch main.tf provider.tf variables.tf outputs.tf
```

Each file serves a specific purpose:
- `main.tf` – main infrastructure resources
- `provider.tf` – AWS provider config
- `variables.tf` – reusable input variables
- `outputs.tf` – final outputs like EC2 public IP

![Created main.tf, variables.tf, provider.tf, outputs.tf](screenshots/03-project-folder-structure-linux.png)

---

### 3. Provider Configuration

In `provider.tf`, I defined the AWS region and provider block:

```hcl
provider "aws" {
  region = var.aws_region
}
```

![Provider file configuration for AWS](screenshots/04-provider-config.png)

---

### 4. Configured AWS CLI

I configured the AWS CLI by entering my Access Key, Secret Key, and default region using the command:

```bash
aws configure
```

![AWS Access/Secret Keys configured](screenshots/05-aws-configure.png)

---

### 5. Installed AWS CLI and Terraform

I installed AWS CLI and Terraform inside WSL (Ubuntu):

```bash
# Install AWS CLI
sudo apt update
sudo apt install awscli -y

# Install Terraform
sudo apt-get install gnupg software-properties-common curl -y
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt install terraform -y
```

![Installed AWS CLI](screenshots/06-aws-cli-installed.png)

![Installed Terraform](screenshots/07-terraform-installed.png)

---

### 6. Initialized Terraform

I ran `terraform init` to initialize the working directory and download the necessary providers and modules.

```bash
terraform init
```

![Terraform Init Command](screenshots/08-terraform-init.png)

![Terraform Backend Initialized](screenshots/09-terraform-init.png)

---

### 7. Created Network Resources

In `main.tf`, I defined:
- A **VPC**
- A **public subnet** and **private subnet**
- An **internet gateway**
- A **route table** and **association**

```hcl
resource "aws_vpc" "main_vpc" {
  cidr_block = "10.0.0.0/16"
  ...
}
```

![VPC, Public and Private Subnets created](screenshots/09-vpc-and-subnets.png)

![Internet Gateway and Routing Configured](screenshots/10-internet-gateway-route-table.png)

---

### 8. Created EC2 Instance and Security Group

I added a **security group** to allow SSH (port 22) and HTTP (port 80), then launched an **EC2 instance** using the Amazon Linux AMI.

```hcl
resource "aws_instance" "web" {
  ami           = "ami-..."
  instance_type = "t2.micro"
  key_name      = var.key_name
  ...
}
```

![Security Group and EC2 Resources](screenshots/11-ec2-instance-and-sg.png)

---

### 9. Terraform Apply

I ran the following command to apply the configuration and create the resources on AWS:

```bash
terraform apply
```

I reviewed the execution plan and typed **yes** to confirm.

![Resources created successfully](screenshots/13-terraform-apply-complete.png)

---

### 10. Verified EC2 Instance on AWS Console

After Terraform finished provisioning, I logged into the AWS Console to confirm that the EC2 instance was running and had a public IP.

![Public IP of EC2 visible](screenshots/14-ec2-public-ip.png)

---

### 11. Connected to EC2 via SSH and Installed Web Server

Using the `.pem` key, I SSH’d into the EC2 instance:

```bash
chmod 400 my-key.pem
ssh -i "my-key.pem" ec2-user@<public-ip>
```

Then I installed Apache:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

![Connected via SSH to EC2](screenshots/15b-ec2-ssh-connected.png)

![Apache installed and verified](screenshots/15c-apache-installed-on-ec2.png)

---

### 12. Output Public IP via Terraform

I configured `outputs.tf` to display the EC2’s public IP address after running `terraform apply`.

```hcl
output "ec2_public_ip" {
  value = aws_instance.web.public_ip
}
```

```bash
terraform output
```

![Output from outputs.tf](screenshots/15-terraform-output.png)

---

### 13. Updated EC2 Resource with Key Name

I created a key pair in AWS, downloaded the `.pem` file, and updated the EC2 config to include the `key_name`.

![Key Pair Created](screenshots/17-keypair-created.png)

![Added key_name to EC2 instance](screenshots/18-main-tf-with-key-name.png)

---

### ✅ Final Test – Web Server

After installing Apache, I opened a browser and navigated to the EC2’s public IP. The test page loaded successfully, confirming that the web server was working.

![Web Server Test - Hello from Oladapo](screenshots/15c-apache-installed-on-ec2.png)

---

## ⚠️ Problems I Faced & Solutions

| Problem | Solution |
|--------|----------|
| **Permission denied when pushing to GitHub** | Configured Git to use the correct email and SSH key |
| **EC2 SSH connection failed** | Updated Security Group to allow inbound port 22 and used correct key |
| **Apache not displaying** | Ensured HTTP (port 80) was open and verified EC2 had a public IP |
| **Terraform apply failed** | Fixed syntax errors and double-checked variable names |

---

## 💡 Lessons Learned

- Infrastructure as Code (IaC) simplifies repeatable cloud setups.
- Security Group rules are essential for connectivity.
- Always verify AWS credentials and region settings.
- Documenting everything helps in automation and troubleshooting.

---

## 🙌 Author

**Oladapo Adenekan**  
🔗 LinkedIn: [www.linkedin.com/in/oladapo568](https://www.linkedin.com/in/oladapo568)

---


