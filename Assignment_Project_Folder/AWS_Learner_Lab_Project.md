# AWS Learner Lab Project Implementation

## [Contents](#contents)

- [Next Steps](#next)
- [Purpose](#purpose)
- [Setup](#setup)
- [Deployment](#deployment)
  - [CloudFormation](#cloudformation-deployment)
  - [Application](#app-deployment)
- [Special Notes](#special-notes)
- [Components](#components)
  - [Network](#network)
    - [VPC](#vpc)
  - [IAM](#iam)
  - [Log](#log)

## [Next](#contents)

- [ ] Document precisely what actions to replicate.
- [ ] Deploy my DORA dash app to the infra.
- [ ] Replace Aurora for RDS MySQL.

## [Purpose](#contents)

The **Learner Lab** is where the assignment project will be built. Need to document the architecture and build. Documentation in relation to development of Module Project in AWS.

## [Setup](#contents)

Both the Lab and Learner Lab environments can be launched at the same time. Have enabled "**multi-session support**". Find at top right of cloud console, drop-down next to **Account-ID**. Learner Lab instance has preferences set to **Dark Theme** to distinguish from other instances.

### Clean-up

To clean-up the workspace, deleting all resources, do the following:

Can just reset the entire environment.

- EC2 > Terminate (delete) instance. Cannot skip OS Shutdown.
- VPC TBC.

## [Deployment](#contents)

Step-by-step deployment run-book.

### [CloudFormation Deployment](#contents)

- Login to AWS Account with browser saved credentials (BPP).
- Start AWS Academy Learner Lab.
- Navigate to CloudFormation.
- Create Stack.
  - With new resources (standard)
- Build from Infrastructure Composer.
  - Create in Infrastructure Composer.
- Select Template (rather than Canvas)
  - Paste in [dora-stack.yaml](./cloudformation/dora-stack.yaml) template.
  - Click "Validate", should go green.
- Create Template.
  - Confirm and continue to CloudFormation.
  - **Next**
- Specify stack details.
  - Enter a stack name = "dora-stack" - or whatever.
  - DBPassword = "password" - change later.
  - KeyPairName = "SPW-SSH" **OR** "vockey- to be used to ssh into servers for deployment.
  - **Next**
- Configure stack options.
  - Ignore this page for now.
  - **Next**
- Review and create.
  - Ignore this page for now.
  - **Submit**
- Monitor
  - "Events" have completed
  - "Resources" == "CREATE-COMPLETE"
- Select "outputs"
  - Copy "WebServerPublicDNS"
  - Paste into browser.
  - Should see app.

### [App Deployment](#contents)

Refer to Learner Lab Instructions: [app_deploy.md](./cloudformation/app_deploy.md).

#### [Connect to ec2 instance](#contents)

These instructions are for Mac/Linux users only.

1. Read through the two bullet points in this step before you start to complete the actions, because you will not be able see these instructions when the AWS Details panel is open.

    - Choose the **i AWS Details** link above these instructions.
    - Choose the **Download PEM** button and save the **labsuser.pem** file.
      - Typically your browser will save it to the Downloads directory.

1. Open a terminal window, and change directory cd to the directory where the .pem file was downloaded.

    - For example, run this command, if it was saved to your Downloads directory:

    ```bash
    cd ~/Downloads
    ```

1. Change the permissions on the key to be read only, by running this command:

    ```bash
    chmod 400 labsuser.pem
    ```

1. Return to the AWS Management Console, and in the EC2 service, choose **Instances**.

    - Check the box next to the instance you want to connect to.

1. In the *Description* tab, copy the **IPv4 Public IP** value.

1. Return to the terminal window and run this command (replace **<public-ip>** with the actual public IP address you copied):

    ```bash
    ssh -i <filename>.pem ec2-user@<public-ip>
    ```

1. Type ***yes*** when prompted to allow a first connection to this remote SSH server.

    - Because you are using a key pair for authentication, you will not be prompted for a password.

#### [Deploy Dash App](#contents)

1. SSH into your EC2 instance as per instructions above.
1. Delete the placeholder folder:

    ```bash
    sudo rm -rf /opt/doraview/*
    ```

1. Clone your repo (N.B. repo is public):

    ```bash
    git clone https://github.com/ingeniousideas/bpp_module2_project.git doraview
    ```

1. Update Directory Trust:

   ```bash
   git config --global --add safe.directory /opt/doraview
   ```

1. Fix Permissions:

    ```bash
    sudo chown -R doraview:doraview /opt/doraview
    ```

1. Install requirements:

    ```bash
    pip3 install -r requirements.txt

#### [Connecting to MySQL Instance](#contents)

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

## [Components](#contents)

### [Network](#contents)

Network configuration. Multi-region redundancy and availability.

#### [VPC](#contents)

- Use a VPC to isolate the application.
- Sub-nets will be used to restrict traffic between components.
- Security Groups to define access rules.

##### [Availability Zones](#contents)

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

##### [NAT Gateway](#contents)

NAT gateway allows private resources to access the internet from any availability zone within a VPC, providing a single managed internet exit point for the entire region. Additional charges apply.

- Using new regional NAT gateway. AWS now offers a multi-AZ NAT Gateway, eliminating the need for separate NAT Gateways across availability zones.

##### [VPC Endpoint](#contents)

Endpoints can help reduce NAT gateway charges and improve security by accessing S3 directly from the VPC. By default, full access policy is used. You can customize this policy at any time.

#### [Load Balancer](#contents)

- Use Load balancer to route traffic between distributed public facing app servers.

### [IAM](#contents)

N.B. Seems creation of User, Groups and Roles is not permitted with current access to the lab.

What IAM has been implemented and how.

Use of the following:

- Users
- Groups
- Roles

## [Log](#contents)

Log what I've been doing to keep track of where I am.

### Mon 09 March

- Design drafted in Miro as [TradeStream](<https://miro.com/app/board/uXjVG0kuU5g=/>)
  - N.B. will open in **Edge**.
- Start Learner Lab Project copying **Lab 2: Build your VPC and Launch a Web Server**.
- Copying with renaming in Learner Lab as basis of my app.
- **Task 1:** Create VPC
  - N. Virginia (us-east-1).

### Sun 12 Apr

- Looking at **Cloudformation** IaC.
  - Try this tutorial <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/gettingstarted.walkthrough.html>
  - Was easy. Template stored  [tutorial_script.yml](./cloudformation/turtorial_script/tutorial_script.yml).
  - Next checking <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-guide.html>.

### Tues 14 Apr

#### Done

- Successfully created working CloudFormation dora_stack.yaml with simple example Dash app.
