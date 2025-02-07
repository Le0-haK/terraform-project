# Azure VNet Arch with Bastion, NSGs & Subnet Isolation

## Description
This project sets up a secure and isolated Azure infrastructure using multiple Virtual Networks (VNets) and subnets. It leverages Azure Bastion for secure RDP/SSH access without exposing public IPs and Network Security Groups (NSGs) for traffic control and isolation.

### Key Features
-> Segregated VNets for HR, IT, and Finance with specific security rules.
-> Azure Bastion Host for secure VM access.
-> Private VMs with no direct internet exposure.
-> Network Security Groups to enforce strict access control.

### Architecture Overview
-> Azure Bastion Host: Provides secure RDP/SSH access without public IPs.
-> HR VNet: SSH (port 22) access is blocked 
-> IT and Finance VNets: SSH access allowed for management
-> NSGs: Implement strict traffic control rules.
-> Virtual Machines: Linux VMs with private IPs and no direct internet access.

## Prerequisites
Terraform installed (>= 4.16.0)
az
Access to an Azure subscription
Service Principal with required permissions

## Setup and Configuration
1. Clone the repo
2. Run this command in your cmd to set the Env variables
'''sh
set "TF_VAR_current_subscription_id=<sub-id>" & set "TF_VAR_current_tenant_id=<tenant-id>"
'''
3.  Generate SSH Key Pair, we need 3 key pairs for each VM
'''sh
ssh-keygen -t rsa -b 2048
'''
4. Add the public key path in the "vm\main.tf" line 32, 88, 144 (Each VM gets assigned its own .pub)

5. Building the config
'''sh
az login  
terraform init  
terraform apply -var-file=tfvars\test.tfvars
'''

## Contributing
Contributions are welcome! Please submit a pull request or raise an issue for any improvements.



