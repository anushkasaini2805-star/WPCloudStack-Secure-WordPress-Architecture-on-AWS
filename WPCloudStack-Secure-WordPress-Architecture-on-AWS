# WPCloudStack-Secure-WordPress-Architecture-on-AWS
We are going to introduce an AWS architecture for an application. This is a complete application that you will build step by step. With each module you complete, you will add a new service or resource to your architecture. But before we start, let's look at the prerequisites.

# Prerequisites
 1. An AWS account with privileges to create IAM roles, AWS VPCs, EC2 instances, and RDS databases.
# Problem
In this lab, you will create the VPC in your AWS account. Before creating a VPC, you need to select a region, considering factors like cost, compliance, and latency. You will also need two subnets in your VPC: a public subnet to host your web application, where you will launch an EC2 instance, and a private subnet to deploy your RDS MySQL database. Then, you will set up the connection between RDS and EC2 and install the WordPress website on the instance. Finally, you will host a simple WordPress website on an EC2 instance and export the static assets to an S3 bucket.

# Architecture
<img width="979" height="590" alt="image" src="https://github.com/user-attachments/assets/7b71b9aa-87ee-4e14-a592-228e8b0cc0b5" />

• Create a VPC within your AWS account. But first, what exactly is a VPC? VPC stands for Virtual Private Cloud, which is a virtual network infrastructure provided by Amazon Web Services (AWS). It allows you to create a logically isolated section of the AWS cloud where you can launch various resources such as EC2 instances, RDS databases, and more. With a VPC, you have complete control over your network configuration, including the ability to define IP address ranges, create subnets, and manage routing tables. You can also establish security groups and network access control lists (ACLs) to regulate the traffic that flows to and from your instances, ensuring a secure environment.

A VPC enables you to extend your data centre into the cloud, providing a seamless and secure connection using an IPsec VPN or AWS Direct Connect. This setup allows for the integration of your VPC with other AWS services, such as Amazon S3 for storage, AWS Lambda for serverless computing, and many others, enhancing the functionality and scalability of your applications.

To get started, follow these steps:

Step 1 – Log in to your AWS account. Once logged in, navigate to the AWS Management Console. In the search bar located at the top of the console, type "VPC" and select the VPC option from the dropdown menu. This will take you to the VPC dashboard, where you can begin setting up your Virtual Private Cloud.


<img width="961" height="362" alt="image" src="https://github.com/user-attachments/assets/e5c55c26-531f-48cc-a53f-21ac29fbeb10" />

Before creating your own VPC, let's understand the default VPC. By default, when you create a new AWS account, a default VPC (Virtual Private Cloud) is automatically set up for you in each AWS region. The default VPC is a logically isolated virtual network within the AWS Cloud that you can use to launch AWS resources, such as EC2 instances, RDS databases, and more. It comes preconfigured with several default settings, including an Internet Gateway and a default subnet in each Availability Zone within the region. This means you can launch your resources in the default VPC without needing to configure networking settings.

<img width="859" height="341" alt="image" src="https://github.com/user-attachments/assets/6ab1d3f5-820e-4aa1-94cc-a151301eea5f" />

Step 2 - Once you are on the VPC dashboard, look for the option to create a new VPC. Click on the "Create VPC" button to start the process. You will be presented with different configuration options. For this step, choose the "VPC only" option, which allows you to create a Virtual Private Cloud without any additional components like subnets or gateways. Next, you need to enter the IPv4 CIDR block, which defines the range of IP addresses that will be available for your VPC. Ensure that you choose a CIDR block that suits your network requirements, keeping in mind the number of resources you plan to deploy within this VPC. Once you have entered the IPv4 CIDR block, review your settings and proceed to create the VPC.

<img width="564" height="676" alt="image" src="https://github.com/user-attachments/assets/0464491b-bc68-4227-ad05-2adb32a63e8d" />

• When you create a new VPC, a Main Route Table is automatically generated for you. This table is crucial for directing network traffic within your VPC. However, by default, it only includes a local route in its target group. This local route allows communication between resources within the VPC but does not enable any external connectivity. If you need your resources to communicate with the internet or other networks, you will need to manually add additional routes to the Main Route Table. These routes can include destinations such as an Internet Gateway for internet access or a Virtual Private Gateway for connecting to a VPN. It's important to carefully configure these routes to ensure that your network traffic is properly managed and secure.

<img width="953" height="394" alt="image" src="https://github.com/user-attachments/assets/370634f3-1d66-47db-a412-14966784de56" />

• Create a Public Subnet in Your Custom VPC

What is a Public Subnet?
A public subnet is a segment of a computer network that is designed to be accessible from the Internet. This means it has a public IP address that allows it to be reached by anyone on the Internet. Public subnets are crucial for deploying resources that need to be accessible to the public, such as web servers, email servers, and other services that require public interaction.

In cloud computing environments, such as Amazon Web Services (AWS), public subnets are often used in conjunction with private subnets to form a Virtual Private Cloud (VPC). This setup allows for a secure and organized network structure. The public subnet is typically used to host resources that need to be accessible from the Internet, providing a gateway for incoming traffic to reach these resources.

On the other hand, the private subnet is reserved for resources that should remain isolated from the public Internet. These resources might include databases, backend servers, and internal applications that require protection from external access. By using both public and private subnets within a VPC, organizations can effectively manage their network traffic, ensuring that public-facing services are accessible while sensitive data and applications remain secure and private.

This dual-subnet configuration allows for a flexible and scalable network architecture, enabling businesses to efficiently manage their resources while maintaining the necessary levels of security and accessibility.

<img width="970" height="267" alt="image" src="https://github.com/user-attachments/assets/4e96ab6b-b25c-4782-9990-9d80b8929c9e" />

In the image above, you can see the subnets that AWS automatically creates when a default VPC is set up. To create a new subnet, follow these steps:

Step 1 – Click on "Create subnet." This will open a form where you can specify the details for your new subnet. First, select your custom VPC from the dropdown menu to ensure the subnet is part of the correct network. Next, give your subnet a meaningful name that reflects its purpose or location within your network architecture.

Then, choose an Availability Zone that suits your needs. This decision might depend on factors such as redundancy, latency, or specific resource requirements. After selecting the Availability Zone, assign an IPv4 CIDR block to the subnet. This block of IP addresses will define the range of addresses available for resources within this subnet. Make sure the CIDR block does not overlap with other subnets in your VPC to avoid IP address conflicts.

By carefully configuring these settings, you can ensure that your subnet is optimally set up to support your application's requirements.

<img width="503" height="689" alt="image" src="https://github.com/user-attachments/assets/1267d9f4-7243-45d6-9613-59bd6a0b31a6" />

Step 2 – Enable the "Auto-assign IP" feature. This setting is crucial because, as the name suggests, it designates the subnet as a Public subnet. By enabling this feature, any new resources launched within this subnet will automatically receive a public IP address. This is important for resources that need to be accessible from the internet, such as web servers or other public-facing applications. Ensuring that this option is enabled will help streamline the deployment process and ensure that your resources are properly configured for external access.

<img width="528" height="635" alt="image" src="https://github.com/user-attachments/assets/3b679922-1084-4bb6-ae7f-3dedf89c89c2" />

Step 3 – Create an Internet Gateway for Your Custom VPC

To effectively connect your Virtual Private Cloud (VPC) to the internet, you need to create an Internet Gateway. But what exactly is an Internet Gateway? An Internet Gateway (IGW) is a crucial component in Amazon Web Services (AWS) that is designed to be horizontally scaled, redundant, and highly available. It serves as a virtual router that facilitates communication between resources within a VPC and the broader internet.

The Internet Gateway acts as a bridge, allowing traffic to flow in both directions. For outbound traffic, it provides a target for data packets that are destined for the public internet from instances within your VPC. This means that any resource, such as a web server, that needs to send data to users or services outside the VPC will route its traffic through the Internet Gateway.

Conversely, for inbound traffic, the Internet Gateway acts as a source for data originating from the internet and intended for instances within your VPC. This is essential for resources that need to be accessible from the outside world, such as public-facing applications or services.

Being an AWS-managed component, the Internet Gateway is attached directly to your VPC. This attachment is what enables the seamless flow of traffic between your VPC and the internet. By setting up an Internet Gateway, you ensure that your VPC can communicate with external networks, thereby extending its functionality and accessibility to users and services across the globe.

<img width="828" height="219" alt="image" src="https://github.com/user-attachments/assets/308cf8e5-d631-4f67-966f-dc042501fd8a" />

In the image above, you can see an Internet Gateway that has already been created. This gateway is automatically set up by AWS when the default VPC is created.

To create a new Internet Gateway, follow these steps:

Click on the "Create Internet Gateway" button in the AWS Management Console. This will initiate the process of setting up a new gateway for your VPC.

Provide a name for your new Internet Gateway. This name will help you identify it easily among other resources in your AWS environment.

After naming your Internet Gateway, proceed by clicking the "Create Internet Gateway" button to finalize the creation process.

Once created, you can attach this Internet Gateway to your VPC, enabling it to handle both inbound and outbound internet traffic for your resources. This setup is crucial for ensuring that your VPC can interact with the internet, allowing your applications and services to be accessible to users and systems outside of your private network.

<img width="663" height="529" alt="image" src="https://github.com/user-attachments/assets/2d5a34d1-f21f-4947-bfcb-1d6c4284ffd7" />

• After successfully creating your new Internet Gateway, the next step is to attach it to your custom VPC. This process is essential as it allows your VPC to handle internet traffic, both incoming and outgoing. To do this, navigate to the "VPC" section in the AWS Management Console. Find your custom VPC from the list of available VPCs. Once you have located it, select the option to "Attach Internet Gateway." You will then be prompted to choose the Internet Gateway you just created. Select it from the list and confirm the attachment. This action will link your Internet Gateway to your VPC, enabling seamless communication between your VPC resources and the internet. This setup is vital for ensuring that your applications and services hosted within the VPC can be accessed by users and systems outside your private network, thereby expanding their reach and functionality.

<img width="806" height="592" alt="image" src="https://github.com/user-attachments/assets/166a598a-1269-4d20-88b5-b339ed7a01bb" />

<img width="828" height="183" alt="image" src="https://github.com/user-attachments/assets/06a3158b-7254-466d-8774-ac6820201a14" />

Step 4 – Add Internet Gateway ID to the Main Route Table

What is a Route Table?

In Amazon Web Services (AWS), a route table is a critical component that determines how network traffic is directed within a Virtual Private Cloud (VPC). When you create a VPC, AWS automatically generates a main route table by default. This main route table is automatically associated with every subnet you create within the VPC unless you choose to associate a subnet with a custom route table instead.

The main route table contains a set of rules, known as routes, that define the paths network traffic should take to reach its destination. These routes are essential for managing how data moves between subnets within the VPC and for controlling access to and from the internet. By default, the main route table includes a route that directs all traffic to a local route, facilitating communication within the VPC itself.

However, to enable resources in a public subnet to access the internet, you need to add a specific route to the main route table. This involves adding a route that directs traffic to an Internet Gateway, which acts as a bridge between your VPC and the internet. Similarly, if you have resources in a private subnet that need internet access, you can add a route to a Network Address Translation (NAT) Gateway. This allows these resources to initiate outbound connections to the internet while remaining inaccessible from the outside world.

You have the flexibility to add, modify, or delete routes in the main route table to tailor the flow of traffic according to your network architecture and security requirements. By carefully configuring these routes, you can ensure that your VPC's resources are accessible as needed while maintaining control over network traffic and security.

<img width="846" height="241" alt="image" src="https://github.com/user-attachments/assets/6cc52824-f127-4e6d-84fe-f45d59a2db15" />

Select route table and go to edit routes in that add destination as 0.0.0.0/0 and past your internet gateway id in target and save the changes.

<img width="901" height="366" alt="image" src="https://github.com/user-attachments/assets/6b4b5c41-50bb-4879-bf7e-06914835276b" />

• To create an EC2 instance in the public subnet of your custom VPC, follow these detailed steps:

Launch Instance: Begin by navigating to the EC2 dashboard in the AWS Management Console. Click on the "Launch Instance" button to start the process of creating a new EC2 instance.

Name Your Instance: Assign a meaningful name to your instance. This name will help you easily identify the instance among others in your AWS environment.

Select Instance Type: Choose an appropriate instance type based on your workload requirements. Instance types vary in terms of CPU, memory, storage, and networking capacity. For example, you might select a t2.micro for a small, low-cost instance or a larger type for more demanding applications.

Create a Key Pair: If you don't already have a key pair, create one. A key pair consists of a public key stored by AWS and a private key file that you store. This key pair is used to securely connect to your instance.

Configure Network Settings: In the network settings section, select your custom VPC from the dropdown menu. Ensure that you choose the public subnet within this VPC. This is crucial because a public subnet allows your instance to communicate with the internet, provided you have configured the necessary routes and Internet Gateway.

Security Group Configuration: Set up a security group to control the inbound and outbound traffic to your instance. For a public instance, you might allow SSH access from your IP address and HTTP/HTTPS traffic if you are hosting a web application.

Review and Launch: Carefully review all your settings to ensure everything is configured correctly. Once you are satisfied, click on the "Launch" button to create your instance.

Connect to Your Instance: After the instance is launched, you can connect to it using the private key file you downloaded earlier. Use an SSH client to establish a secure connection.

By following these steps, you will successfully create an EC2 instance in the public subnet of your custom VPC, ready for deployment and accessible from the internet.

<img width="623" height="710" alt="image" src="https://github.com/user-attachments/assets/545f3617-a6a7-4438-8f26-4adb98558e73" />

• Create a Private Subnet in Your Custom VPC

In Amazon Web Services (AWS), a private subnet is a part of a VPC that doesn't have a direct route to the Internet, meaning it isn't linked to an Internet Gateway. Instances in a private subnet can communicate with other instances in the same VPC or with other VPCs through a VPN or VPC peering connection. Typically, resources needing high security, like databases, backend servers, or internal applications, are placed in private subnets. Since they aren't directly accessible from the Internet, they are less exposed to public Internet attacks. They can only be accessed by authorized users or resources within the same VPC.

Step 1 – Click on "Create a Subnet," then select your custom VPC. Name the subnet, choose an availability zone, and assign an IPv4 CIDR block to this subnet.

<img width="507" height="632" alt="image" src="https://github.com/user-attachments/assets/1b28dc84-9cb4-42e0-8546-e7ef262c87d8" />


Note:

Auto-assign IP will be disabled because, as the name suggests, it is a private subnet.

An Internet gateway is not required since it is a private subnet.

Step 2 – Create a route table and keep only local targets in it.

<img width="455" height="407" alt="image" src="https://github.com/user-attachments/assets/83c8f0e7-5c04-4361-8cb5-6f6fa864bc17" />

<img width="637" height="584" alt="image" src="https://github.com/user-attachments/assets/234d9ac9-d219-435f-a5f9-53658517f074" />

In below image you can see resource map, Public subnets are attached to Route table and Internet gateway, where Private subnets are attached to only Route table without Internet gateway access.

<img width="631" height="303" alt="image" src="https://github.com/user-attachments/assets/ea096317-32bd-47fb-b700-fe741c39db16" />


•Create an RDS MySQL database in the private subnet of a custom VPC. RDS (Relational Database Service) is a web service from AWS (Amazon Web Services) that simplifies setting up, operating, and scaling a relational database in the cloud. RDS supports various database engines, including MySQL, PostgreSQL, Oracle, and SQL Server. It allows users to manage databases in the cloud without needing extensive hardware or software resources. RDS offers automated backups, software patching, and scalable storage, making it an efficient and cost-effective database management solution. When using RDS in AWS, users can choose from different instance types, which determine the computing and memory capacity of the database instance. RDS also supports read replicas, enabling users to create multiple copies of their database for read-intensive workloads.

Step 1 - Before creating RDS, first create a subnet group consisting only of private subnets in RDS.

<img width="730" height="444" alt="image" src="https://github.com/user-attachments/assets/59ed7674-5f5d-40a7-aa25-3e184edcaef8" />
Step 2 – Create database by click on create database.

<img width="721" height="245" alt="image" src="https://github.com/user-attachments/assets/a7efdde1-329b-4cc6-9277-63208a62e393" />

Step 3 – Select Standard create, choose mysql and version, and I select free tier template

<img width="728" height="627" alt="image" src="https://github.com/user-attachments/assets/4b120e60-1d61-4153-8638-e2cf550afe20" />

Step 4 – In setting type a name for your database, type master username and type of password.

<img width="719" height="417" alt="image" src="https://github.com/user-attachments/assets/c2f82aef-cfd5-4e30-9c6d-cfd675ec528d" />
Step 5 – In Instance configuration select Db instance class and select storage type and size.

<img width="695" height="393" alt="image" src="https://github.com/user-attachments/assets/e9ab60d7-c191-4aaf-a3e7-d260fa32277b" />


Step 6 – In connectivity choose your VPC and Public access NO.

<img width="714" height="455" alt="image" src="https://github.com/user-attachments/assets/6284156f-bec7-49f0-ad80-1197e99752ec" />

Step 7 – Select Database authentication as password authentication, and click on click on database

<img width="726" height="461" alt="image" src="https://github.com/user-attachments/assets/ca8c1a99-5a33-4161-8c92-fa2188e8ed0a" />

<img width="736" height="177" alt="image" src="https://github.com/user-attachments/assets/38173a9d-920c-49c2-9698-7cfee83dd8a1" />

Step 8 - Now, let's move on and modify the security groups for the RDS and EC2 instances. We need an EC2 instance, so please create one along with any missing AWS resources we've set up so far.

Select public-instance-sg.

Click the "Edit inbound rules" button.

Click "Add rule." For Type, select MYSQL/Aurora.

For Source, select custom and find assg-rds-mysql-sg, then click "Save rules."

Click "Add rule." For Type, select HTTP.

For Source, select My IP, and click "Save rules."

<img width="731" height="298" alt="image" src="https://github.com/user-attachments/assets/bcf90218-0c4d-4f41-9d81-48664620971a" />

Select db-sg.

Click the "Edit inbound rules" button.

Delete the existing rule.

Click "Add rule." For Type, select MYSQL/Aurora.

For Source, select custom and find public-instance-sg, then click "Save rules."

<img width="713" height="252" alt="image" src="https://github.com/user-attachments/assets/3e7f2d59-b862-4ab8-8921-f73cb0b2b0d7" />

Create an S3 bucket with a unique name.
Step 1 – Search for S3 in the search bar and create an S3 bucket with the name “assg-bucket-”.
<img width="730" height="352" alt="image" src="https://github.com/user-attachments/assets/902abf02-9160-4418-9e81-580d1070b7ef" />

Step 2 – Block Public Access to this bucket and click on create bucket.

<img width="726" height="342" alt="image" src="https://github.com/user-attachments/assets/de27d612-5a8c-4a8d-b397-3ab41d53373b" />

<img width="740" height="206" alt="image" src="https://github.com/user-attachments/assets/3daed33b-9415-4c76-b135-01d63b9a5870" />


• Set Up the WordPress Environment

Step 1 - Select the public instance and click "Connect." On the "Connect to instance" page, click "SSH client" in the menu, and you will find the connection command in the example.

• Windows Users: Follow the steps in this guide to connect to the EC2 instance using PuTTY.

• MacOS Users: Open a terminal on your computer, navigate to the folder where your .pem key file is stored, and paste the connection command.

<img width="728" height="254" alt="image" src="https://github.com/user-attachments/assets/8c7bd9a9-957a-47fb-946e-a5a8bad7360a" />

Step 2 - After successfully connecting, run the following commands to install the LAMP stack (Linux, Apache, MariaDB, and PHP) on your instance:

sudo yum install httpd -y

sudo service httpd start

sudo service httpd status

sudo yum install mariadb-server -y

sudo service mariadb start

sudo service mariadb status

sudo amazon-linux-extras install php8.0 -y

sudo service php-fpm start

sudo service php-fpm status

sudo service httpd restart

sudo service mariadb restart

sudo service php-fpm restart

Here, I'm installing LAMP using a shell script, and we need to give execute permission to that LAMP file.

<img width="631" height="306" alt="image" src="https://github.com/user-attachments/assets/4d2e6907-13e7-45c7-a0ea-6886cce1aaf7" />

<img width="733" height="143" alt="image" src="https://github.com/user-attachments/assets/a1c5fc91-59b5-4d95-9688-c7b11521ef69" />

Step 3 - Set the MySQL environment variable on your computer. Replace it with the endpoint found in the RDS console for your database. Use the following command:
sudo mysql -h [endpoint] -u [username] -p
Then, create a database named database1.

<img width="772" height="299" alt="image" src="https://github.com/user-attachments/assets/623bf4e8-638e-4591-a345-39474f6f303e" />

Step 4 – Navigate to the html directory using the command cd /var/www/html. Then, download the WordPress module and unzip it with the following commands:

wget https://wordpress.org/latest.tar.gz

tar -xzf latest.tar.gz

<img width="727" height="427" alt="image" src="https://github.com/user-attachments/assets/021aa3d8-2ec0-478b-b1da-6657bb0c3473" />

Step 5 - Go into the WordPress folder and back up the default config file using the following commands:

cd wordpress
cp wp-config-sample.php wp-config.php
<img width="718" height="105" alt="image" src="https://github.com/user-attachments/assets/b0d41576-359f-44dd-a4c7-f32c643d4aba" />


Step 6 - After that, use nano to edit the wp-config.php file with the command: nano wp-config.php

Step 7 - Change the following values in the script:

DB_NAME: 'wordpress'

DB_USER: 'wordpress'

DB_PASSWORD: 'wordpress-pass'

DB_HOST: your RDS endpoint

Then, save the file.

<img width="725" height="396" alt="image" src="https://github.com/user-attachments/assets/778482cf-6a69-4621-9e8c-16d41480d577" />
Step 8 - Select the EC2 instance, find the Public IPv4 DNS in the Details section below, and paste it into your browser. You will then see the WordPress setup page. On the setup page, enter your own values for Site Title, Username, Password, and Your Email, then click Install WordPress.

<img width="725" height="362" alt="image" src="https://github.com/user-attachments/assets/f0a96a37-a735-4e08-aff9-202feb4c1613" />

• After a few seconds, it will redirect to the Login page.
• Enter your username and password, and click the Login button to see the admin page.
• You can use the Admin dashboard to enhance your blog.
• Now, you can view your blog in your browser.

<img width="600" height="302" alt="image" src="https://github.com/user-attachments/assets/f95ea1be-0daf-426e-b3b1-ad2ad4416569" />

Congratulations on successfully hosting a WordPress website on an EC2 instance! By following the steps outlined, you have configured all the necessary AWS services to get your site up and running. This process involved downloading and setting up WordPress, configuring the database connection, and ensuring that your EC2 instance is properly linked with your RDS database. You also learned how to edit configuration files and navigate the WordPress setup page to customize your site with a unique title, username, password, and email address.

Once the setup was complete, you accessed the WordPress admin dashboard, where you can manage and enhance your blog with various themes and plugins. This dashboard is a powerful tool that allows you to customize the appearance and functionality of your site to suit your needs.

If you encounter any issues or have further questions about managing your WordPress site or AWS services, feel free to leave a message here. We are here to help you with any challenges you might face as you continue to develop and improve your website.


