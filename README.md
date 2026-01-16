IAC on TERRAFORM
•	Infrastructure as a code tool.
•	Use to automate Infra as a reusable tool 
•	Cost saving
•	Reuse for multiple time (using IAC) 
•	Using 	 help  of workspaces
	CloudFormation :  service 
•	Stats created 	
•	Only on aws automation creates 	
•	Cloud native services 	
	Terraform :  over multiple cloud 
	Ansible :  configuration management tool inside Infra
	Shellscript : pure IAC tool 	
-------------------------------------------------------------------------------------------------------	
TERRAFORM
•	Open source platform 
•	Developed by HASSICORP
•	Is an IAC tool used to provision and manage Infra using configuration files	
•	creates updates and delete infrastructure.
•	 HCL language
•	Code  on  Tf  →configuration file
•	Work  on Block type


i.	 Terraform: library block/ folder
ii.	provider aws/Gcp/ azure  -> cloud wender connect
iii.	Resource -> what resource can be created
iv.	Data ->  existing cloud resource
             default infrastructure resource 	
             used directly on code.
v.	Variable: set global Variable 
vi.	Module : code reuses again and again in these block 
vii.	Output: Inwritten Value (DNS/ARN/IP,etc) prints on terminal 	
--------------------------------------------------------------------------------------------------------
	Difference between cloudFormarion and terraform 
Feature	AWS CloudFormation	Terraform
Provider support	AWS only	Multi-cloud (AWS, Azure, GCP, Kubernetes, GitHub, etc.)
Language	JSON / YAML	HCL (HashiCorp Configuration Language)
Learning curve	Steeper (verbose syntax)	Easier & more readable
State management	Managed by AWS automatically	Managed via state file (terraform.tfstate)
Multi-cloud support	❌ No	✅ Yes
Modules / Reusability	Limited	Strong module system
Dependency handling	Implicit & explicit	Automatic dependency graph
Drift detection	Limited	Excellent (terraform plan)
Community & ecosystem	AWS-centric	Very large & active
Cost	Free (AWS service)	Free (Open-source), paid enterprise features
CI/CD integration	AWS native tools	Works with all CI/CD tools
-------------------------------------------------------------------------------------------------------
	Advantages of Infrastructure as Code (IaC)
1️⃣ Automation
•	Infrastructure is created automatically using code
•	Reduces manual configuration and human errors
2️⃣ Consistency & Standardization
•	Same code = same infrastructure every time
•	Avoids configuration drift between environments (Dev / QA / Prod)
3️⃣ Version Control
•	Infrastructure code can be stored in Git
•	Easy to track changes, rollback, and audit
4️⃣ Faster Deployment
•	Infrastructure provisioning takes minutes instead of hours/days
•	Ideal for CI/CD pipelines
5️⃣ Scalability
•	Easily scale resources by changing code
•	Supports dynamic infrastructure growth
6️⃣ Documentation
•	Code itself acts as documentation
•	Easier for new team members to understand infrastructure
7️⃣ Disaster Recovery
•	Infrastructure can be recreated quickly in case of failure
•	Improves reliability and business continuity
_------------------------------------------------------------------------------------------------------_______________________________________
Advantages of Terraform (as an IaC Tool)
1️⃣ Multi-Cloud Support
•	Works with AWS, Azure, GCP, Kubernetes, GitHub, Datadog, etc.
•	Avoids vendor lock-in
2️⃣ Declarative Language (HCL)
•	You define what you want, not how
•	Simple, readable, and easy to learn
3️⃣ Execution Plan (terraform plan)
•	Shows exact changes before applying
•	Helps prevent accidental deletions or misconfigurations
4️⃣ State Management
•	Tracks real infrastructure using a state file
•	Detects drift between code and actual resources
5️⃣ Dependency Management
•	Automatically creates resources in correct order
•	Builds dependency graph internally
6️⃣ Reusable Modules
•	Write once, reuse many times
•	Encourages best practices and clean architecture
7️⃣ Strong Community & Providers
•	Thousands of providers and modules
•	Extensive documentation and community support
8️⃣ CI/CD Friendly
•	Easily integrates with Jenkins, GitHub Actions, GitLab CI, etc.
-------------------------------------------------------------------------------------------------------
	Create  EC2 instance (Ubuntu)
	Modify IAM role 
	On console 
sudo-i
apt update –y
wget  (paste the installation link of terraform given below) https://releases.hashicorp.com/terraform/1.14.3/terraform_1.14.3_linux_amd64.zip
ls
apt install unzip 
unzip terraform_1.14.3_linxu_amd64.zip
ls
pwd
rm –rvf  terraform_1.14.3_linxu_amd64.zip
mv terraform /bin 
ls
terraform –version
vim ec2.tf 
------------------------------------------------------------------------------
		provider "aws" {
   	      		 region = "us-east-2"
}
resource "aws_instance" "my-ec2"{
ami = “ami-000e44536tshy4689”
  			 instance_type = “t3.micro”
    			key_name = “SR”
 security_groups = ["default"]
tags = {
 		    Name = "my-server"
}
}
-----------------------------------------------------------------------------
ls
ls –a
terraform init
terraform plan
terraform apply 
ls
vim ec2.tf 
	------same but ami id and imag =  linux ----------
terraform plan 
terraform apply –auto-approve
ls
terraform destroy –auto-approve

Refresh instances to see one more instance is displayed using the linux image 

------------------------------------------------------------------------------------------------------------
LIFECYCLE
1.	Write the code 
2.	Initialize the TERRAFORM
3.	TERRAFORM plan
4.	TERRAFORM apply 
5.	TERRAFORM destroy
------------------------------------------------------------------------------------------------------------
	BLOCK 
I.	Variable block
II.	Heredoc 
III.	Output block 
IV.	Data block 
-------------------------------------------------------------------------------------------------------
	Launch instance (UBUNTU)
	Modify IAM role 
	Console 
sudo –i 
apt update –y
wget  (paste the installation link of terraform given below) https://releases.hashicorp.com/terraform/1.14.3/terraform_1.14.3_linux_amd64.zip
ls
apt install unzip 
unzip terraform_1.14.3_linxu_amd64.zip
ls
pwd
rm –rvf  terraform_1.14.3_linxu_amd64.zip
mv terraform /bin
ls
terraform –version
apt update 
vim main.tf 
--------------------------------------------------------------------------------------------------------
	provider "aws" {
  	      region = "us-east-2"
}





resource "aws_instance" "my-ec2"{
 	        ami = var.image-id
        instance_type = var.instance-type
        key_name = var.my-key
        security_groups = ["default"]
tags = {
 	    Name = "my-server"
}
}
vim var.tf 
	variable "image-id" {
   	    type = string
  	    description = "this var block is for ami id"
  	    default = "ami-0f5fcdfbd140e4ab7"
}
variable "instance_type" {
   	     type = string
 	     description = "this var block is for ami id"
   	     default = "t3.micro"
}
variable "my-key" {
   	    type = string
    	    description = "this var block is for ami id"
   	    default = "ohio-soheb-key"
}
----------------------------------------------------------------------------------------------
----Refresh instance to see one more added
terraform init
terraform plan
terraform apply –auto-approve
vim main.tf
-----------------------------------------------------------------------------------------------
	provider "aws" {
  	      region = "us-east-2"
}





resource "aws_instance" "my-ec2"{
 	        ami = var.image-id
        instance_type = var.instance-type
        key_name = var.my-key
        security_groups = ["default"]
	user_data = <<-EOT
    #!/bin/bash
    yum update -y
    yum install httpd -y
    systemctl start httpd
    systemctl enable httpd
    EOT
tags = {
 	    Name = "my-server"
}
}
-----------------------------------------------------------------------------------------------
terraform apply –auto-approve
vim output.tf
--------------------------------------------------------------------------------------------
	output "instance_public_ip" {
 	value = aws_instance.my-ec2.public_ip
 	description = "Public IP address of the instance."
}
--------------------------------------------------------------------------------------------
terraform plan
terraform apply –auto-approve
vim main.tf 
	---------------------------------------------------------------------------
	resource "aws_security_group" "my-sg" {
  	 	 name = "my-sg2"
    		description = "allow all traffic"

 tags = {
     		 Name = "my-new-sg"
    	}
ingress {
   	 from_port = 22
    	  to_port = 22
  	  protocol = "tcp"
   	  cidr_blocks = ["0.0.0.0/0"]
}
ingress {
    	  from_port = 80
  	  to_port = 80
   	  protocol = "tcp"
   	  cidr_blocks = ["0.0.0.0/0"]
}
egress {
   	   from_port = 0
    	   to_port = 0 
    	   protocol = "-1"
    	   cidr_blocks = ["0.0.0.0/0"]
}
}
provider "aws" {
  	      region = "us-east-2"
}

resource "aws_instance" "my-ec2"{
 	        ami = var.image-id
       	        instance_type = var.instance-type
        	        key_name = var.my-key
       	       # security_groups = ["default"]
       vpc_security_group_ids = [aws_security_group.my-sg.id]	user_data = <<-EOT
 	           #!/bin/bash
           yum update -y
           yum install httpd -y
           systemctl start httpd
           systemctl enable httpd
                       EOT
tags = {
 	    Name = "my-server"
}
}
-----------------------------------------------------------------------------------------------------------------
terraform plan
terraform apply –auto-approve 
	see on instances – sg rules 


