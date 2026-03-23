# AWS Foundations > Module 5 > Lab 2

## [Contents](#contents)

- [Objective](#objective)
- [Setup](#setup)
- [Tutorial](#tutorial)

## [Objective](#contents)

Build a VPC and Launch a Web Server.

- Leverage tutorials to understand how to implement simple components.
- In parallel, implement tutorial features in [AWS Academy Learner Lab](https://awsacademy.instructure.com/courses/157159).
- Learner Lab work will documented separately in [AWS_Learner_Lab_Project](/Assignment_Project_Folder/AWS_Learner_Lab_Project.md).

### [Lab Outline](#contents)

Use the VPC and more option in the VPC console to create multiple resources:

- a **VPC**,
- an **Internet Gateway**,
- a **public subnet**
- and a **private subnet** in a **single Availability Zone**,
- two **route tables**,
- and a **NAT Gateway**.

## [Setup](#contents)

Both the Lab and Learner Lab environments can be launched at the same time. Have enabled "**multi-session support**". Find at top right of cloud console, drop-down next to **Account-ID**. Learner Lab instance has preferences set to **Dark Theme** to distinguish from other instances.

### AWS Resource Access

- **Tutorial:** [Foundations: Module 5: Lab - 2 Build your VPC and Launch a Web Server](https://awsacademy.instructure.com/courses/157155/assignments/1863762?module_item_id=15325849
)
- **Assignment working space:** [AWS Academy Learner Lab](https://awsacademy.instructure.com/courses/157159)

## [Tutorial](#contents)

### [Create VPC](#contents)

Virtual defined network. Benefits using scale of AWS. VPC can span multiple Availability Zones. Additional subnets are added to this.

In the top right of the screen, verify that N. Virginia (us-east-1) is the region. 

Choose the VPC dashboard link which is towards the top left of the console.

Next, choose Create VPC. 

Note: If you do not see a button with that name, choose the Launch VPC Wizard button instead.

  

Configure the VPC details in the VPC settings panel on the left:

Choose VPC and more.

Under Name tag auto-generation, keep Auto-generate selected, however change the value from project to lab.

Keep the IPv4 CIDR block set to 10.0.0.0/16

For Number of Availability Zones, choose 1.

For Number of public subnets, keep the 1 setting.

For Number of private subnets, keep the 1 setting.

Expand the Customize subnets CIDR blocks section

Change Public subnet CIDR block in us-east-1a to 10.0.0.0/24

Change Private subnet CIDR block in us-east-1a to 10.0.1.0/24

Set NAT gateways to In 1 AZ.

Set VPC endpoints to None.

Keep both DNS hostnames and DNS resolution enabled.

 

In the Preview panel on the right, confirm the settings you have configured.

VPC: lab-vpc

Subnets:

us-east-1a

Public subnet name: lab-subnet-public1-us-east-1a

Private subnet name: lab-subnet-private1-us-east-1a

Route tables

lab-rtb-public

lab-rtb-private1-us-east-1a

Network connections

lab-igw

lab-nat-public1-us-east-1a

[Create subnets](#contents)

[Configure a security group](#contents)

[Launch EC2 instance in to VPC](#contents)
