# Guidance on connecting and deploying app

## Accessing EC2 Instances

When launching EC2 instances in the default us-east-1 Region in this environment, choose the option to use the existing key pair named vockey at the time of launch.  Then:

- Choose the AWS Details link above these instructions.

  - If you are using a Windows desktop or laptop, choose the **Download PPK** button and save the **labsuser.ppk** file. You can use this file to connect via SSH to a Linux EC2 instance or Windows EC2 instance, typically using a tool such as PuTTY.
  - If you are using a MacOS desktop or laptop, choose the **Download PEM** button and save the **labsuser.pem** file. You can use this file to connect via SSH to a Linux EC2 instance or Windows EC2 instance, typically using a terminal window.

- To connect via Remote Desktop to a Windows EC2 instance:
  - In the EC2 Console, choose **Instances** and choose the instance you want to connect to
  - From the **Actions** menu choose **Get Windows Password**
  - Next to Key Pair Path choose **Browse**.
  - Browse to and select the labsuser.pem file you downloaded earlier.
  - Choose **Decrypt Password**.
  - The connection information will now display, including the instance's Public DNS, Administrator user name, and the decrypted password.
  - Use a Remote Desktop Protocol (RDP) client to connect to the desktop of the EC2 instance using these connection details.
  - **To connect using SSH to a Linux instance, see the next section.**

## SSH access to an EC2 Instance you launch

The steps below describe how to use the SSH key to connect to your instance.

Tip: Assuming you launched the instance with the vockey key pair, and that you have opened TCP port 22 in the instance's security group, you can also SSH to an EC2 instance by using the terminal to the side of these instructions. The terminal already has the key pair available to it. Simply enter the command ssh -i ~/.ssh/labsuser.pem ec2-user@<public-ip> where <public-ip> is the actual IPv4 public address of the instance.

### Windows Users: Using SSH to Connect

**These instructions are for Windows users only.**

1. Download needed software.
    - You will use PuTTY to SSH to Amazon EC2 instances. If you do not have PuTTY installed on your computer, download it here.
1. Open putty.exe
1. Configure PuTTY to not timeout:
    - Choose Connection
    - Set Seconds between keepalives to 30. This allows you to keep the PuTTY session open for a longer period of time.
1. Configure your PuTTY session:
    - Choose Session
    - **Host Name (or IP address):** Copy and paste the **IPv4 Public IP address** for the instance. To find it, return to the EC2 Console and choose **Instances**. Check the box next to the instance and in the Description tab copy the **IPv4 Public IP value**.
    - Back in PuTTy, in the **Connection** list, expand  **SSH**
    - Choose **Auth** (don't expand it)
    - Choose **Browse**
    - Browse to and select the .ppk file that you downloaded
    - Choose **Open** to select it
    - Choose **Open**
1. Choose **Yes**, to trust the host and connect to it.
1. When prompted **login as**, enter: ***ec2-user***. This will connect you to the EC2 instance.

### macOS  and Linux  Users - Using SSH to Connect

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
