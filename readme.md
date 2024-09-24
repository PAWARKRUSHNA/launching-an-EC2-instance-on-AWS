Creating an EC2 instance on AWS using the AWS CLI (Command Line Interface) involves several steps. Below is a detailed step-by-step guide with code snippets that you can use directly in your GitHub repository.

# Step 1: Install AWS CLI on Windows
Download the AWS CLI MSI installer for Windows from the AWS CLI Installation page.
Run the installer and follow the on-screen instructions.
Description: This step installs the AWS Command Line Interface, allowing you to manage AWS services from the command line.

# Step 2: Configure AWS CLI
After installing, you need to configure the AWS CLI with your AWS credentials.

Open Command Prompt (cmd) and run the following command:
```
aws configure
```
Description: This command will prompt you to enter your AWS Access Key ID, Secret Access Key, default region name, and output format. These configurations allow the AWS CLI to authenticate your requests.

# Step 3: Create a Key Pair
Create a key pair that will allow you to securely connect to your EC2 instance. Run the following command in Command Prompt:
```
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem

```
Description: This command creates a new key pair named "MyKeyPair" and saves the private key to MyKeyPair.pem. Keep this file secure, as it is necessary for accessing your instance.

# Step 4: Set Permissions for the Key Pair
On Windows, you do not need to change permissions for the key pair file like on Unix-based systems. However, ensure that the file is stored securely.

Description: It’s crucial to keep your key pair file safe, as it is required for SSH access to your EC2 instance.

# Step 5: Launch an EC2 Instance
Use the following command to launch an EC2 instance. Replace <ami-id> with the appropriate Amazon Machine Image (AMI) ID for your desired operating system and <subnet-id> with your actual subnet ID.
```
aws ec2 run-instances --image-id <ami-id> --count 1 --instance-type t2.micro --key-name MyKeyPair --subnet-id <subnet-id> --associate-public-ip-address
```
Description: This command launches a new EC2 instance with the specified AMI ID and instance type. The --associate-public-ip-address option allows the instance to be reachable over the internet.

# Step 6: Verify Instance Launch
You can check the status of your instances with the following command:
```
aws ec2 describe-instances --filters "Name=key-name,Values=MyKeyPair"
```
Description: This command retrieves information about instances associated with your key pair, allowing you to confirm that the instance has launched successfully.

# Step 7: Connect to Your EC2 Instance
Once your instance is running, you can connect to it using SSH. First, you need a terminal that supports SSH, such as Git Bash or Windows Terminal. Replace <ec2-public-ip> with the public IP address of your EC2 instance.

Open Git Bash or Windows Terminal and run:
```
ssh -i MyKeyPair.pem ec2-user@<ec2-public-ip>
```
Description: This command establishes a secure shell connection to your EC2 instance using the private key you created earlier. Make sure to replace <ec2-public-ip> with the actual public IP address of your instance.

Complete Code Snippet
You can copy the following code and add it to your GitHub repository in a Markdown file (README.md or any other descriptive file) for future reference:
# AWS EC2 Instance Creation Guide for Windows

## Step 1: Install AWS CLI on Windows
1. Download the AWS CLI MSI installer for Windows from the [AWS CLI Installation page](https://aws.amazon.com/cli/).
2. Run the installer and follow the on-screen instructions.

## Step 2: Configure AWS CLI
Open Command Prompt (cmd) and run the following command:
bash
```aws configure```

# Step 3: Create a Key Pair
Run the following command in Command Prompt:
```
aws ec2 run-instances --image-id <ami-id> --count 1 --instance-type t2.micro --key-name MyKeyPair --subnet-id <subnet-id> --associate-public-ip-address

```
# Step 4: Set Permissions for the Key Pair
On Windows, you do not need to change permissions for the key pair file, but ensure it is stored securely.
# Step 5: Launch an EC2 Instance
Run the following command, replacing <ami-id> and <subnet-id> with actual values:
```
aws ec2 run-instances --image-id <ami-id> --count 1 --instance-type t2.micro --key-name MyKeyPair --subnet-id <subnet-id> --associate-public-ip-address

```
# Step 6: Verify Instance Launch
Check the status of your instances with:
```
aws ec2 describe-instances --filters "Name=key-name,Values=MyKeyPair"

```
# Step 7: Connect to Your EC2 Instance
Open Git Bash or Windows Terminal and run:
```
ssh -i MyKeyPair.pem ec2-user@<ec2-public-ip>
```
### Notes
- Replace `<ami-id>` and `<subnet-id>` with actual values from your AWS account.
- Ensure your AWS account has permissions to create EC2 instances.
- You may need to adjust your security group settings to allow SSH access (port 22).













