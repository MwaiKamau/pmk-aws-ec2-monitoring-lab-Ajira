<img width="2560" height="1440" alt="Launching-Your-Amazon-EC2-Instance" src="https://github.com/user-attachments/assets/bb23e00e-c0c1-4e0c-bc2c-ac0e7af1079e" />
<img width="1097" height="932" alt="ec2-instance-connect-endpoint-1" src="https://github.com/user-attachments/assets/df21d4e6-3f75-44e8-8611-a2225e6846b0" />
<img width="1000" height="469" alt="instance_storage" src="https://github.com/user-attachments/assets/46bf36c7-7503-4171-b765-a6af80653b04" />
![PMK-AWS-Ajira-Alarm](https://github.com/user-attachments/assets/c1f111ad-eb2b-4049-af34-bf8cfdde3e9a)
![PMK-AWS-Ajira-Alarm-03](https://github.com/user-attachments/assets/80435c53-f424-4274-bed9-1f9822e561de)

Here is a detailed, step-by-step guide to creating your first EC2 instance. This tutorial is designed for absolute beginners and includes instructions for publishing on GitHub and Medium (see also notes on how to save the screenshots for later use).

Creating Your First Amazon EC2 Instance: A Complete Beginner's Guide
Section 1: Project Title and Description

"AWS EC2 Hands-On: Launch Your First Virtual Server with Monitoring & Alerts"
Project Description

This project is a comprehensive, hands-on introduction to Amazon Web Services (AWS) Elastic Compute Cloud (EC2). As a beginner or novice cloud practitioner, you will learn how to launch your first virtual server (an EC2 instance) in the cloud. You will then configure professional-grade monitoring using Amazon CloudWatch to track the server's CPU performance and set up an email alert system using Amazon Simple Notification Service (SNS). Finally, you will simulate a high server load to trigger a real-time alert, giving you practical experience in cloud operations. By the end of this tutorial, you will have successfully built a mini cloud monitoring system, a fundamental skill for any cloud engineer.

Section 2: Architecture Overview
Before we start clicking, it's crucial to understand the AWS building blocks we'll be using. The diagram below illustrates the infrastructure we will create.
+-----------------------------------------------------------------------+
|                           AWS Cloud                                    |
|  +-----------------------------------------------------------------+  |
|  |                        AWS Region (e.g., US East N. Virginia)   |  |
|  |                                                                 |  |
|  |  +--------------------------+    +----------------------------+  |  |
|  |  |     Default VPC          |    |       CloudWatch           |  |  |
|  |  |  (Virtual Private Cloud) |    |  (Monitoring Service)      |  |  |
|  |  |                          |    |                            |  |  |
|  |  |  +-------------------+   |    |  +----------------------+  |  |  |
|  |  |  |   Public Subnet   |   |    |  |      Alarm           |  |  |  |
|  |  |  |  (in AZ us-east-1a)|   |    |  | (Triggers when CPU  |  |  |  |
|  |  |  |                   |   |    |  |    > 70% for 5 min)  |  |  |  |
|  |  |  |  +-------------+  |   |    |  +----------+-----------+  |  |  |
|  |  |  |  | EC2 Instance |<----|----|------------|--------------|  |  |  |
|  |  |  |  | (t2.micro)   |  |   |    |            |              |  |  |  |
|  |  |  |  +-------------+  |   |    |            |              |  |  |  |
|  |  |  |        ^          |   |    +------------|--------------+  |  |  |
|  |  |  +--------|----------+   |                 |                 |  |  |
|  |  |           |              |                 v                 |  |  |
|  |  |  +--------|----------+   |    +----------------------------+  |  |  |
|  |  |  |  Internet Gateway |   |    |            SNS             |  |  |  |
|  |  |  |     (IGW)         |   |    |   (Notification Service)  |  |  |  |
|  |  |  +--------^----------+   |    |                            |  |  |  |
|  |  +-----------|--------------+    |  +----------------------+  |  |  |  |
|  |              |                   |  |       Topic          |  |  |  |  |
|  +--------------|-------------------|--| (HighCPUAlerts)      |  |  |  |  |
|                 |                   |  +----------+-----------+  |  |  |  |
|                 |                   |             |              |  |  |  |
+-----------------|-------------------|-------------|--------------+  |  |
                  |                   |             |                 |  |
                  |                   |             v                 |  |
                  |                   |    +-------------------+      |  |
                  |                   |    |  Email Subscription|      |  |
                  |                   |    | (your@email.com)  |      |  |
                  |                   |    +-------------------+      |  |
                  |                   |                               |  |
                  v                   v                               v  |
            (Your Computer)    (Your Inbox)                (Your Phone)  |
Let's break down each component                                          |
Virtual Private Cloud (VPC): This is your private, isolated section of the AWS cloud. Think of it as your own data centre in the cloud. For this project, we'll use the Default VPC, which AWS automatically creates for you. It comes with a pre-configured internet gateway and subnets, making it perfect for beginners.

Subnet: A subnet is a range of IP addresses within your VPC. A subnet lives in a single Availability Zone. We will launch our EC2 instance in a Public Subnet, which means it will have internet access, allowing us to connect to it from our computer.

Internet Gateway (IGW): This is a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet. The default VPC already has one attached.

EC2 Instance: This is our virtual server. We'll be launching a t2.micro instance, which is eligible for the AWS Free Tier.

CloudWatch: This is AWS's monitoring service. We will create a CloudWatch Alarm that constantly watches the CPU Utilization metric of our EC2 instance.

SNS (Simple Notification Service): This is a managed pub/sub messaging service. We will create an SNS Topic and subscribe our email address to it. When the CloudWatch alarm is triggered, it will send a message to this topic, which will then be forwarded to our email.
Section 3: Step-by-Step Setup Instructions
Prerequisites
An AWS account. If you don't have one, go to aws.amazon.com and sign up. You will need a credit card to verify your identity, but you will not be charged as long as you stay within the Free Tier limits.

Step 1: Launch an EC2 Instance
Log in to the AWS Management Console.

In the "Find Services" search bar, type EC2 and select it to open the EC2 Dashboard.

On the EC2 Dashboard, click the big orange "Launch Instance" button.

(Screenshot Suggestion: EC2 Dashboard with "Launch Instance" button highlighted)

Name your instance: In the "Name and tags" section, enter MyFirstEC2Instance.

Choose an Amazon Machine Image (AMI): An AMI is a template for your server's operating system. Under "Application and OS Images," select Quick Start. Choose Amazon Linux (or Amazon Linux 2) and make sure the AMI is marked "Free Tier eligible".

(Screenshot Suggestion: The AMI selection area, showing "Amazon Linux" and "Free tier eligible" highlighted)

Choose an Instance Type: This defines the hardware of your server. Under "Instance type," select t2.micro, which is also Free Tier eligible.

(Screenshot Suggestion: Instance type selection with t2.micro highlighted)

Create a Key Pair (Login): This is crucial for security. It's like a digital key to securely connect to your server.

Under "Key pair (login)," select "Create new key pair".

Give it a name, e.g., my-first-keypair.

For "Key pair type," leave it as RSA.

For "Private key file format," choose .pem (this works for Linux, Mac, and OpenSSH on Windows).

Click "Create key pair". Your browser will automatically download the .pem file. SAVE THIS FILE IN A SAFE PLACE. You will not be able to download it again.

(Screenshot Suggestion: The "Create key pair" pop-up window)

Network Settings:

Under "Network settings," click the "Edit" button.

By default, AWS will select your "Default VPC" and a "Default subnet." This is perfect for our project.

For "Auto-assign public IP," ensure it is set to Enable.

Under "Firewall (security groups)," select "Create security group". This is your virtual firewall. We will allow SSH (for Linux) to connect to the server. Name the security group my-first-sg.

Under "Inbound security groups rules," add a rule:

Type: SSH

Source: My IP (This automatically adds your current IP address, which is a good security practice).

(Screenshot Suggestion: Network settings section with the new SSH rule shown)

Configure Storage: Under "Configure storage," you will see a root volume of 8 GiB (gibibytes). This is the disk space for your server. The t2.micro instance comes with 30 GiB of free storage for EBS volumes, so this setting is fine.

Launch the Instance: Review the summary panel on the right and click the "Launch instance" button at the bottom of the page.

Success! You will see a success message. Click the instance ID (e.g., i-1234567890abcdef0) to go to the Instances page, where you can see your server starting up. Its state will go from Pending to Running.

Step 2: Create an SNS Topic for Alerts
In the AWS search bar, type SNS and select Simple Notification Service.

On the SNS dashboard, click "Create topic".

Under "Details," select Standard (which is the default).

In "Name," enter HighCPUAlerts .

Click the "Create topic" button at the bottom.

You will be taken to your new topic's page. Click the "Create subscription" button.

Create a Subscription:

Topic ARN: This should already be filled in.

Protocol: Select Email.

Endpoint: Enter your email address (the one you want to receive alerts at).

Click "Create subscription".

Confirm your subscription: Go to your email inbox. You will see an email from "AWS Notifications" with the subject "AWS Notification - Subscription Confirmation". Open it and click "Confirm subscription" . You will see a confirmation page in your browser.

(Screenshot Suggestion: The AWS SNS subscription confirmation email)

Step 3: Create a CloudWatch Alarm
In the AWS search bar, type CloudWatch and select it.

In the left-hand navigation pane, under "Alarms," click "All alarms".

Click the orange "Create alarm" button.

Select Metric: Click "Select metric".

Navigate to: EC2 -> Per-Instance Metrics.

In the list of metrics, find your running instance. You can search for it using the name you gave it, MyFirstEC2Instance. Check the box next to the metric called CPUUtilization and click "Select metric".

(Screenshot Suggestion: The CloudWatch "Select metric" screen with CPUUtilization highlighted for the specific instance)

Configure Alarm:

Under "Conditions," define the alarm trigger:

For is, leave it as > (greater than).

For CPUUtilization, enter 70 (this is the threshold).

Under "Additional configuration," for "Datapoints to alarm," ensure it's 1 out of 1.

For "Missing data treatment," select "Treat missing data as missing" (or "ignore").

Click Next.

Configure Actions:

Under "Alarm state trigger," make sure "In alarm" is selected.

Under "Select an SNS topic," choose "Select an existing SNS topic".

Under "Send a notification to...," select the topic you created, HighCPUAlerts.

Click Next.

Add Name and Description:

Alarm name: High-CPU-Alarm

Alarm description: Alarm when CPU exceeds 70% for 1 datapoint within 1 minute.

Click Next.

Preview and Create: Review the settings and click "Create alarm".

Step 4: Test the Alarm
Now, let's simulate a high workload on our server to see the monitoring system in action!

Go back to the EC2 Instances page.

Select your running instance (MyFirstEC2Instance). Click the "Connect" button at the top.

You'll see the "Connect to instance" page. Select the "EC2 Instance Connect" tab. This is a browser-based SSH client. Click the "Connect" button.

A terminal window will open inside your browser. You are now logged into your Linux server!

Generate CPU Load: In the terminal, copy and paste the following command and press Enter:

dd if=/dev/zero of=/dev/null &
This command creates a high CPU load by reading from /dev/zero (which generates infinite zeros) and writing it to /dev/null (which discards it). The & runs it in the background.

Monitor the Alarm:

Go back to the CloudWatch console and click "All alarms".

After about 2-3 minutes, you will see your High-CPU-Alarm change from OK to In alarm.

Check your email! You should receive an email from AWS with the subject "ALARM: 'High-CPU-Alarm' in US East...".

(Screenshot Suggestion: The CloudWatch Alarms page showing the alarm in the "In alarm" state)
(Screenshot Suggestion: The SNS alert email in your inbox)

Stop the CPU Load: In the terminal window where you're connected to your EC2 instance, run this command to stop the high CPU process:

killall dd
After a few minutes, the CloudWatch alarm will automatically return to the OK state as the CPU utilization drops.

Section 4: Screenshots of Project

(In your actual GitHub or Medium article, you would paste your screenshots here. The descriptions below indicate what the reader should see.)

Screenshot 1: EC2 Instance Running

Description: A screenshot of the AWS EC2 Instances page.

Visuals: The page should show one instance named "MyFirstEC2Instance" with an "Instance State" of "Running" and "Status Checks" showing "2/2 checks passed".

Screenshot 2: CloudWatch Alarm in ALARM State

Description: A screenshot of the Amazon CloudWatch "All Alarms" page.

Visuals: The alarm named "High-CPU-Alarm" should have a state of "In alarm". The graph on the page should clearly show the CPU utilization spiking above the red threshold line (set at 70%).

Screenshot 3: SNS Email Notification Received

Description: A screenshot of your email inbox.

Visuals: An email from "AWS Notifications" is open. The subject line reads something like ALARM: "High-CPU-Alarm" in US East (N. Virginia). The email body contains details about the alarm, including the metric (CPUUtilization), the threshold (70%), and the instance ID

Section 5: Lessons Learned / What I Would Do Differently

This project was an excellent introduction to core AWS services. Here are my key takeaways and what I would improve next time:

Start with the Default VPC: 
For absolute beginners, the default VPC is a lifesaver. It abstracts away the complexity of configuring internet gateways and route tables, letting you focus on the core EC2 and monitoring concepts.

EC2 Instance Connect is a Game-Changer: 
I loved using EC2 Instance Connect to connect to my Linux instance. It's a secure, browser-based SSH client that doesn't require you to manage the private .pem key in a terminal. It's perfect for quick experiments and for novices.

Monitoring is Deceptively Simple: 
Setting up a CloudWatch alarm was incredibly easy, but I learned that its true power lies in configuration. The next step would be to set up an Auto Scaling Group. This service would use a CloudWatch alarm like the one we created to automatically launch new EC2 instances if the CPU load gets too high, and terminate them when it drops—making the application truly scalable and resilient.

Cost Awareness: 
While the Free Tier covers the t2.micro instance and basic CloudWatch alarms, it was a good reminder to always terminate instances when they are not in use. The killall dd command stopped the load, but leaving the instance running would eventually incur charges after the Free Tier expires. I will add a reminder to clean up resources in future guides.

Section 6: AWS Services Used and Their Purpose

Service				Purpose in this Project

Amazon EC2:	The core compute service. We launched a virtual server (EC2 instance) to run our workload. This is the "what" of our project. 

Amazon VPC:	The networking layer. We used the Default VPC to provide a logically isolated network for our EC2 instance, including an internet gateway for public access. This is the "where" of our project.
 
Amazon CloudWatch	The monitoring service. We created a CloudWatch Alarm to watch the CPUUtilization metric of our EC2 instance. It continuously collects and analyzes performance data.
 
Amazon SNS	The notification service. We created an SNS Topic and subscribed our email address to it. When the CloudWatch alarm was triggered, it sent a message to the topic, which was then forwarded to our inbox. 

How to Publish on GitHub & Medium

For GitHub:

Create a new repository named aws-ec2-first-instance-monitoring.

Add a README.md file. Copy the entire content of this guide (sections 1-6) into the README.md.

Add a /screenshots folder. Upload the three screenshots you took into this folder.

Update the image links in your README. Instead of (Screenshot Suggestion...), use markdown like [EC2 Instance Running](./screenshots/ec2-running.png).

Commit and push the changes.

For Medium:

Create a new story.

Paste the content. Copy the text from this guide into the Medium editor.

Upload your images. Use the Medium editor's image tool to upload the three screenshots and place them in the correct sections (under Section 4).

Format. Use the heading options (H1, H2, H3) to format the section titles. Use backticks (`) to format code and commands (like dd if=/dev/zero of=/dev/null &).

Add a "Tags" section. Add tags like AWS, CloudComputing, EC2, DevOps, Beginner, and Tutorial.
