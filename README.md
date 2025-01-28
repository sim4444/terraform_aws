# 4640-w4-lab-start-w25


See lab instructions on D2L for details

This lab demonstrates the process of creating a basic AWS infrastructure using Terraform. The goal was to provision a VPC, subnet, internet gateway, route table, security group, and an EC2 instance running Ubuntu 24.04. The lab also included configuring SSH access and ensuring best practices for file security.

Steps Performed
1. Setting Up the Environment
Installed and configured Terraform on my local machine.
Verified access to AWS using valid credentials in the ~/.aws/credentials file.
Created the Terraform configuration file (main.tf) with all required infrastructure components.
2. Infrastructure Provisioning
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
Secured the private key (do-key) by using the command:
chmod 600 do-key
Ensured that the private key had the correct permissions before attempting to SSH into the instance.
4. Terraform Commands Used
Initialized Terraform to download the AWS provider plugin:
terraform init
Validated the configuration:
terraform validate
Planned the changes:
terraform plan
Applied the changes to provision the resources:
terraform apply

5. Outputs
Configured Terraform to output the instance's public IP and DNS name for quick access:
output "instance_ip_addr" {
  description = "The public IP and DNS of the web EC2 instance."
  value = {
    "public_ip" = aws_instance.web.public_ip
    "dns_name"  = aws_instance.web.public_dns
  }
}

Clone this repository:

git clone <repo-url>
cd 4640-w4-lab
Initialize Terraform:
terraform init
Review the plan:
terraform plan
Apply the configuration:
terraform apply
SSH into the EC2 instance using the private key:
ssh -i do-key ubuntu@<public_ip>


Acknowledgments
HashiCorp Terraform Documentation: https://developer.hashicorp.com/terraform
AWS Terraform Provider Docs: https://registry.terraform.io/providers/hashicorp/aws/latest
