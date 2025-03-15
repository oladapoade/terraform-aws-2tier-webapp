
# Terraform 2-Tier Web App on AWS

This project demonstrates how I deployed a 2-tier architecture (VPC, subnets, security group, and EC2 instance) using **Terraform** on **AWS**. It includes the setup, Terraform configuration, encountered challenges, and solutions.

---

## 📁 Project Structure

The project is organized using separate Terraform configuration files:

![Initial Terraform project structure](screenshots/01-project-folder-structure.png)


---

## 🛠️ Tools Used

- **Terraform**
- **AWS CLI**
- **Visual Studio Code** with **WSL (Ubuntu)** on Windows

---

## 🚀 Step-by-Step Guide

### 1. Installed Visual Studio Code and Launched WSL

![VS Code Installed](screenshots/01-vscode-installed.png)

![WSL Ubuntu inside VS Code](screenshots/02-ubuntu-terminal-in-vscode.png)


---

### 2. Created Project Folder and Files

![Created main.tf, variables.tf, provider.tf, outputs.tf](screenshots/03-project-folder-structure-linux.png)


---

### 3. Provider Configuration

![Provider file configuration for AWS](screenshots/04-provider-config.png)


---

### 4. Configured AWS CLI

![AWS Access/Secret Keys configured](screenshots/05-aws-configure.png)


---

### 5. Installed AWS CLI and Terraform

![Installed AWS CLI](screenshots/06-aws-cli-installed.png)

![Installed Terraform](screenshots/07-terraform-installed.png)


---

### 6. Initialized Terraform

![Terraform Init Command](screenshots/08-terraform-init.png)

![Terraform Backend Initialized](screenshots/09-terraform-init.png)


---

### 7. Created Network Resources

![VPC, Public and Private Subnets created](screenshots/09-vpc-and-subnets.png)

![Internet Gateway and Routing Configured](screenshots/10-internet-gateway-route-table.png)


---

### 8. Created EC2 Instance and Security Group

![Security Group and EC2 Resources](screenshots/11-ec2-instance-and-sg.png)


---

### 9. Terraform Apply

![Resources created successfully](screenshots/13-terraform-apply-complete.png)


---

### 10. Verified EC2 Instance on AWS Console

![Public IP of EC2 visible](screenshots/14-ec2-public-ip.png)


---

### 11. Connected to EC2 via SSH and Installed Web Server

![Connected via SSH to EC2](screenshots/15b-ec2-ssh-connected.png)

![Apache installed and verified](screenshots/15c-apache-installed-on-ec2.png)


---

### 12. Output Public IP via Terraform

![Output from outputs.tf](screenshots/15-terraform-output.png)


---

### 13. Updated EC2 Resource with Key Name

![Key Pair Created](screenshots/17-keypair-created.png)

![Added key_name to EC2 instance](screenshots/18-main-tf-with-key-name.png)


---

### ✅ Final Test

![Web Server Test - Hello from Oladapo](screenshots/15c-apache-installed-on-ec2.png)


---

## ⚠️ Problems I Faced & Solutions

| Problem | Solution |
|--------|----------|
| Terraform GitHub push permission denied to wrong user | I updated my GitHub config to use the correct email/account |
| SSH key permissions too open | Ran `chmod 400 my-key.pem` to restrict access |
| EC2 connection failed initially | Fixed by adding correct key name to EC2 resource and security group rule |
| Apache page not loading | Ensured Security Group allowed HTTP (port 80) & EC2 had public IP |

---

## 💡 Lessons Learned

- Always verify your AWS credentials and Terraform backend before deployment.
- Managing infrastructure as code makes cloud resource provisioning repeatable and scalable.
- EC2 security requires both correct permissions and network config (VPC, routes, security group).

---

## 🙌 Author

**Oladapo Adenekan**  
LinkedIn: [www.linkedin.com/in/oladapo568](https://www.linkedin.com/in/oladapo568)

---

