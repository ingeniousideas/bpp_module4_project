# AWS Learner Lab Project Implementation

## [Contents](#contents)

- [Purpose](#purpose)
- [Setup](#setup)
- [Special Notes](#special-notes)
- [Network](#network)
  - [VPC](#vpc)
- [IAM](#iam)
- [Log](#log)

## [Purpose](#contents)

The **Learner Lab** is where the assignment project will be built. Need to document the architecture and build. Documentation in relation to development of Module Project in AWS.

## [Setup](#contents)

Both the Lab and Learner Lab environments can be launched at the same time. Have enabled "**multi-session support**". Find at top right of cloud console, drop-down next to **Account-ID**. Learner Lab instance has preferences set to **Dark Theme** to distinguish from other instances.

## [Target Infrastructure](#contents)

### My Iteratively Developed Design

![Iterative HLD](/Assignment_Project_Folder/AWS_HLD_Workings.drawio.svg)

### Reference Designs from Lectures etc

![Subnets & Routes](/AWS_ArchDiagrams/AWS_SubNetsRouting.png)

![Basic Lab App](/AWS_ArchDiagrams/AWS_BasicLabApp.png)

![Three Tier App](/AWS_ArchDiagrams/AWS_3TierNetworkinge.png)

## [Special Notes](#contents)

Have created an IAM User for use in the Lab.

- **User Name:**
  - SPW-Lab-Admin
- **Password:**
  - *See Secure Credentials Store.*
  - *Registered under "**Platform Credentials**"*
- **Group:**
  - Lab-Admin

## [Network](#contents)

Network configuration. Multi-region redundancy and availability.

### [VPC](#contents)

- Use a VPC to isolate the application.
- Sub-nets will be used to restrict traffic between components.
- Security Groups to define access rules.

#### [Availability Zones](#contents)

- use1-az1 (us-east1a)
- use1-az2 (us-east1b)

Public Sub-nets = 2

Private Sub-nets = 4

Custom CIDR Ranges. Each with 256 IPs.

- 10.0.0.0.24
- 10.0.0.1.24
- 10.0.0.2.24
- 10.0.0.3.24
- 10.0.0.4.24
- 10.0.0.5.24

#### [NAT Gateway](#contents)

NAT gateway allows private resources to access the internet from any availability zone within a VPC, providing a single managed internet exit point for the entire region. Additional charges apply.

- Using new regional NAT gateway. AWS now offers a multi-AZ NAT Gateway, eliminating the need for separate NAT Gateways across availability zones.

#### [VPC Endpoint](#contents)

Endpoints can help reduce NAT gateway charges and improve security by accessing S3 directly from the VPC. By default, full access policy is used. You can customize this policy at any time.

### [Load Balancer](#contents)

- Use Load balancer to route traffic between distributed public facing app servers.

## [IAM](#contents)

N.B. Seems creation of User, Groups and Roles is not permitted with current access to the lab.

What IAM has been implemented and how.

Use of the following:

- Users
- Groups
- Roles

## [Log](#contents)

Log what I've been doing to keep track of where I am.

- **Mon 09 March**
  - Design drafted in Miro as [TradeStream](<https://miro.com/app/board/uXjVG0kuU5g=/>)
    - N.B. will open in **Edge**.
  - Start Learner Lab Project copying **Lab 2: Build your VPC and Launch a Web Server**.
  - Copying with renaming in Learner Lab as basis of my app.
  - **Task 1:** Create VPC
    - N. Virginia (us-east-1).
