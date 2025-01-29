# 4640-w4-lab-start-w25

This lab shows the process of creating a basic AWS infrastructure using Terraform.

Steps Performed
1. Setting Up the Environment
Installed and configured Terraform on my local machine.
Verified access to AWS using valid credentials in the ~/.aws/credentials file.
Created the Terraform configuration file (main.tf) with all required infrastructure components.

## Created a New SSH Key Pair

 -created an SSH key pair for accessing the EC2 instance:

1. Use the following command to generate a new SSH key pair:
   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f do-key
   ```
   
3. Infrastructure Provisioning
I edited the Terraform configuration (main.tf) to set up the following AWS resources:

a. VPC
Created a VPC (10.0.0.0/16) to serve as the base network for my resources.
Enabled DNS support and hostnames for the VPC.

b. Public Subnet
Created a subnet (10.0.1.0/24) in the us-west-2a availability zone.
Enabled public IP allocation for instances launched in this subnet.

c. Internet Gateway
Attached an internet gateway to the VPC to enable external connectivity.

d. Route Table
Configured a route table to route external traffic (0.0.0.0/0) through the internet gateway.
Associated the route table with the public subnet.

e. Security Group
Created a security group to allow:
SSH traffic (port 22) from anywhere.
HTTP traffic (port 80) from anywhere.
All outbound traffic.

f. EC2 Instance
Used the latest Ubuntu 24.04 AMI owned by Amazon.
Provisioned a t2.micro instance in the public subnet.
Associated the security group with the EC2 instance.
Configured a cloud-init script (cloud-config.yaml) to customize the instance during boot.

3. Key Pair Security
   
- Secured the private key (do-key) by using the command:
```bash
chmod 600 do-key
```
Ensured that the private key had the correct permissions before attempting to SSH into the instance.

5. Terraform Commands Used:
   
a. Initialized Terraform to download the AWS provider plugin:
```bash
terraform init
```

b. Validated the configuration:
```bash
terraform validate
```

c. Planned the changes:
```bash
terraform plan
```

d. Applied the changes to provision the resources:
```bash
terraform apply
```

e. SSH into the EC2 instance using the private key:
```bash
ssh -i do-key web@<public_ip>
```


Acknowledgments
HashiCorp Terraform Documentation: https://developer.hashicorp.com/terraform
AWS Terraform Provider Docs: https://registry.terraform.io/providers/hashicorp/aws/latest
