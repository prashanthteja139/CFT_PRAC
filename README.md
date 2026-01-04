# AWS EC2 Deployment Automation using CloudFormation & AWS CLI

## 📌 Project Overview
This repository contains a **project-level Infrastructure as Code (IaC) solution** to automate deployment of an **Amazon EC2 instance** using:
- **AWS CloudFormation (YAML template)**
- **AWS CLI for stack lifecycle automation**
- **Security Group managed inside the template for drift-traceable network configuration**
- **Parameter inputs for reusable deployments**
- **Outputs for instance ID and public IP**
- **Tagging aligned with corporate cloud governance**

## 🏗 AWS Resources Provisioned
| CloudFormation Resource | Description |
|---|---|
| `AWS::EC2::Instance` | Deploys an EC2 VM in AWS |
| `AWS::EC2::SecurityGroup` | Enables SSH (22) and HTTP (80) access |
| `Parameters` | Allows users to pass Instance Type, AMI ID, Key Pair, and Environment |
| `Outputs` | Returns Instance ID and Public IP after deployment |

---

## ⚙ Required User Inputs (Replace These)
Users must provide values for the following:

```yaml
Parameters:
  InstanceType  → EC2 compute size (Example: t3.micro)
  AmiId         → AMI ID based on region
  KeyPairName   → Existing AWS Key Pair name (Example: my-keypair)
  Environment   → Tag for environment (Example: Dev / QA / Prod)
⚠ Important: The Key Pair must already exist in AWS. Do not include .pem in the template, only the Key Pair name.

🚀 Deploy CloudFormation Stack using AWS CLI
Run the deployment script or execute the command manually:

Option 1 — Using script:
bash
Copy code
chmod +x deploy.sh
./deploy.sh
Option 2 — Manual CLI command:
bash
Copy code
aws cloudformation create-stack \
  --stack-name <STACK_NAME> \
  --template-body file://template.yaml \
  --parameters \
      ParameterKey=InstanceType,ParameterValue=<INSTANCE_TYPE> \
      ParameterKey=AmiId,ParameterValue=<AMI_ID> \
      ParameterKey=KeyPairName,ParameterValue=<KEY_PAIR_NAME> \
      ParameterKey=Environment,ParameterValue=<ENV_NAME> \
  --region <AWS_REGION>
Example:

bash
Copy code
aws cloudformation create-stack \
  --stack-name demo-ec2-stack \
  --template-body file://template.yaml \
  --parameters \
      ParameterKey=InstanceType,ParameterValue=t3.micro \
      ParameterKey=AmiId,ParameterValue=ami-1234567890abcdef0 \
      ParameterKey=KeyPairName,ParameterValue=my-keypair \
      ParameterKey=Environment,ParameterValue=Dev \
  --region us-east-1
🔍 Get Stack Outputs after Deployment
bash
Copy code
aws cloudformation describe-stacks \
  --stack-name <STACK_NAME> \
  --query "Stacks[0].Outputs" \
  --region <AWS_REGION>
🧹 Delete Stack (Terminates EC2 and SG created by this stack)
bash
Copy code
chmod +x delete.sh
./delete.sh
Or manually:

bash
Copy code
aws cloudformation delete-stack --stack-name <STACK_NAME> --region <AWS_REGION>
🧩 Key Skills Demonstrated
Infrastructure automation using CloudFormation (IaC)

Cloud deployment through AWS CLI

Managed network state using Security Groups in IaC

Reusable infra using CloudFormation Parameters

Stack lifecycle control using Shell scripting

Cloud governance using Tags & Outputs

Linux + SSH operational familiarity

🔐 Security Best Practice for Users (Add this later)
Create a .gitignore file to avoid committing private keys:

bash
Copy code
*.pem
.env
.aws/
🎯 Ideal Roles This Project Supports
Cloud Engineer • AWS Infrastructure Support • Cloud Solutions • Site Reliability • Cloud Automation Roles

✍ Author
Chakri (Chakradhar Seeramsetty)
Cloud Infrastructure Automation Project

yaml
Copy code

---

If you want, next I can also generate:
- a **parameterized version of your CloudFormation template**
- architecture diagram (Mermaid)
- GitHub badges for skills

Just say **"continue"** when ready.






