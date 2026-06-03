If your goal is to **actually perform the experiment and deploy an EC2 instance using Terraform on AWS**, follow this complete step-by-step guide.

# Experiment No. 10

# Deployment of End-to-End Architecture using Terraform on AWS

## Prerequisites

Before starting, make sure you have:

* AWS Account
* Windows Laptop/Desktop
* Internet Connection
* Administrator Access

---

# Step 1: Create AWS Account

1. Open AWS website:

   [https://aws.amazon.com](https://aws.amazon.com)

2. Click **Create AWS Account**

3. Complete registration

4. Add payment details

5. Verify phone number

6. Login to AWS Console

---

# Step 2: Create IAM User for Terraform

### Open

AWS Console → IAM

### Create User

1. IAM → Users
2. Click **Create User**
3. Username:

```text
terraform-user
```

4. Next

---

### Attach Permissions

Select:

```text
AdministratorAccess
```

For educational purposes only.

Click:

```text
Create User
```

---

### Generate Access Keys

Open created user

Go to:

```text
Security Credentials
```

Click:

```text
Create Access Key
```

Select:

```text
Command Line Interface (CLI)
```

Download:

```text
Access Key ID
Secret Access Key
```

Save them safely.

---

# Step 3: Install AWS CLI

Download:

[https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)

Install AWS CLI.

Verify installation:

```bash
aws --version
```

Expected:

```bash
aws-cli/2.x.x
```

---

# Step 4: Configure AWS CLI

Open Command Prompt

Run:

```bash
aws configure
```

Enter:

```bash
AWS Access Key ID:
```

Paste your Access Key.

```bash
AWS Secret Access Key:
```

Paste Secret Key.

```bash
Default region:
```

Example:

```bash
us-east-1
```

Output format:

```bash
json
```

---

Verify:

```bash
aws sts get-caller-identity
```

If successful you will see:

```json
{
 "UserId":"...",
 "Account":"...",
 "Arn":"..."
}
```

---

# Step 5: Install Terraform

Download Terraform:

[https://developer.hashicorp.com/terraform/downloads](https://developer.hashicorp.com/terraform/downloads)

Download Windows AMD64 version.

Extract ZIP.

Example:

```text
C:\Terraform
```

Contains:

```text
terraform.exe
```

---

# Step 6: Add Terraform to PATH

### Environment Variables

Add:

```text
C:\Terraform
```

to System PATH.

Restart CMD.

Verify:

```bash
terraform -version
```

Example:

```bash
Terraform v1.8.x
```

---

# Step 7: Create Project Folder

Create folder:

```text
Terraform-AWS
```

Open CMD inside folder.

---

# Step 8: Create Terraform File

Create:

```text
main.tf
```

Paste:

```terraform
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {

  ami           = "ami-053b0d53c279acc90"
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformInstance"
  }
}
```

---

# Step 9: Initialize Terraform

Run:

```bash
terraform init
```

Terraform downloads AWS Provider.

Expected:

```text
Terraform has been successfully initialized
```

---

# Step 10: Validate Configuration

Run:

```bash
terraform validate
```

Expected:

```text
Success! The configuration is valid.
```

---

# Step 11: Check Deployment Plan

Run:

```bash
terraform plan
```

Terraform shows:

```text
1 to add
0 to change
0 to destroy
```

No resources are created yet.

---

# Step 12: Deploy Infrastructure

Run:

```bash
terraform apply
```

Terraform asks:

```text
Do you want to perform these actions?
```

Type:

```text
yes
```

Press Enter.

Terraform creates:

```text
EC2 Instance
```

Expected:

```text
Apply complete!
```

---

# Step 13: Verify on AWS Console

Go to:

```text
AWS Console
```

Then:

```text
EC2
```

Then:

```text
Instances
```

You should see:

```text
TerraformInstance
```

Status:

```text
Running
```

---

# Step 14: Get Instance Information

Run:

```bash
terraform show
```

You can see:

* Instance ID
* Public IP
* Private IP
* Region

---

# Step 15: Save Infrastructure State

Terraform automatically creates:

```text
terraform.tfstate
```

This file stores resource information.

Do not delete it.

---

# Step 16: Destroy Infrastructure (Important)

After experiment completion:

```bash
terraform destroy
```

Type:

```text
yes
```

Terraform removes EC2 instance.

Expected:

```text
Destroy complete
```

This avoids AWS charges.

---

# Viva Questions

### What is Terraform?

Terraform is an Infrastructure as Code (IaC) tool used to automate cloud infrastructure deployment.

---

### What is IaC?

Infrastructure as Code is the process of managing infrastructure using code instead of manual configuration.

---

### What command initializes Terraform?

```bash
terraform init
```

---

### What command shows execution plan?

```bash
terraform plan
```

---

### What command deploys resources?

```bash
terraform apply
```

---

### What command deletes resources?

```bash
terraform destroy
```

---

### What is AWS EC2?

Amazon Elastic Compute Cloud (EC2) is a virtual machine service provided by AWS.

---

### What file stores Terraform state?

```text
terraform.tfstate
```

---

# Expected Result

**An EC2 instance was successfully deployed on Amazon Web Services using Terraform. The infrastructure was created automatically through Terraform configuration files, demonstrating Infrastructure as Code (IaC) and cloud resource automation.**
