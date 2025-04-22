# A step by step buide on how to configure load balancer in AWS

 There are 7 main setups you need to configure on the AWS platform to achieve this, and they are:
VPC
Internet Gateway
Subnet
Route table
EC2 instance (2 instances)
Target group
Load Balancer


## VPC
•	Search and select VPC from the search bar.

![1](https://github.com/user-attachments/assets/7eb79f7f-87ef-4fc5-97b0-d8f9934ab8a4)

•	On the VPC dashboard, click on ‘Create VPC’.
![2](https://github.com/user-attachments/assets/ba8dc783-7330-4040-b96e-b8b0ee0f083d)

•	Select ‘VPC only’, create a name tag for your VPC, fill in an IP address range (for this guide, you’ll be using 20.0.0.0/16), and then click ‘Create VPC’
![3](https://github.com/user-attachments/assets/6b08d29f-5ec8-4720-a192-9b8a59063c9b)


•	Your VPC has been successfully created
![4](https://github.com/user-attachments/assets/ef5d9ffe-dee7-4382-9c22-a75d30972f82)



## Internet Gateway
•	On the left pane of the VPC dashboard, click on ‘Internet gateways,’ then click on ‘Create Internet gateway.’
![5](https://github.com/user-attachments/assets/cd119a3c-435c-49ec-8dde-1f143583571a)

•	Create your desired name tag. Leave the remaining options as is and click ‘Create Internet Gateway.’ 
![6](https://github.com/user-attachments/assets/0126ba75-8041-463d-bef8-89c869b686da)


•	On the newly created internet gateway page, you will see that the State is ‘Detached.’ To attach it to your VPC, click the ‘Actions’ button and select ‘Attach to VPC’
![7](https://github.com/user-attachments/assets/f377e507-62b3-4a15-8cef-eb3cebf08be8)

•	Click the search bar, select your VPC, and click ‘Attach internet gateway’
![8](https://github.com/user-attachments/assets/c9544f6b-1cf6-4a82-90bb-9a6c734fd6c3)


•	Check the state; you’ll see it’s attached now.
![9](https://github.com/user-attachments/assets/b6f777f5-673c-45ec-b0ae-9d52168853ac)



## Subnet
You need to create 2 subnets for the 2 VPCs you’ll be creating to test the load balancer.

•	On the VPC dashboard's left pane, click ‘Subnets.’ You’ll see different subnets in the subnet menu, but for the sake of this guide, let’s create a new one.
![10](https://github.com/user-attachments/assets/3037928d-3c6c-4664-b64d-4b2c0c863b3f)


•	Click on the VPC ID drop-down and select your VPC.
![11](https://github.com/user-attachments/assets/2f4991eb-6afe-4b18-9805-a9a8d25cff35)


•	Fill in your subnet name.
![12](https://github.com/user-attachments/assets/1b44ff97-94bf-44a7-ae13-92b3fc9174a5)


•	Click the ‘Availability zone’ dropdown, and for this subnet, you’ll use ‘us-east-1a’.
![13](https://github.com/user-attachments/assets/2f3a5eab-14ec-4895-9118-d3b6ae4dc455)


•	In the IPv4 subnet CIDR block, use the subnet range ‘20.0.1.0/24.’ Next, click the ‘add new subnet’ button to create the second subnet you’ll be working with.
![14](https://github.com/user-attachments/assets/0df24a85-f73c-4cf6-89c0-64e699b014a6)


•	Follow the same steps to create the new subnet, save for a few changes:
o	Fill in a different name for his subnet
o	Click the ‘Availability zone’ dropdown, and for this subnet, you’ll be using ‘us-east-1b’.
o	In the IPv4 subnet CIDR block, use the subnet range 20.0.3.0/24. Once done, click ‘Create subnet.’
![15](https://github.com/user-attachments/assets/9c092121-9d65-4071-8803-021f3eb9511d)


•	You have successfully created the new subnets
![16](https://github.com/user-attachments/assets/cfc32ed4-635f-4a17-ada8-a01e871b615d)



## Route Tables
Here, you’ll be configuring the Route Table to help the public subnet have access to the internet.

•	On the VPC dashboard's left pane, click ‘Route tables’. 
![17](https://github.com/user-attachments/assets/fcc3e0cc-95ee-48a4-8c06-e3e7c0b208c4)



•	Create a name for your route table, select the VPC you created earlier, and click on the ‘create route table’ button.
![18](https://github.com/user-attachments/assets/20546d1b-0259-42c1-a369-5a4fdaddac55)


•	On your newly created route table dashboard, click the Subnet Associations tab. Click on the ‘Edit Subnet Association’ button
![19](https://github.com/user-attachments/assets/69994590-d4b4-487c-93f5-64b197eea08e)


•	Select both subnets you created earlier and click on ‘Save associations.’
![20](https://github.com/user-attachments/assets/0cc4ca08-cc23-4be5-aa6d-14e44b308122)



•	On the route table dashboard, go to the route tab and click on ‘edit routes.’
![21](https://github.com/user-attachments/assets/77feb2cb-c392-4550-a5e0-a28ef029b48f)


•	Click on the ‘add route’ button, and under the destination column, click on the search bar and select 0.0.0.0/0. Next, under the target column, click on the drop-down and select ‘Internet gateway.’
![22](https://github.com/user-attachments/assets/ca4f2026-a6ea-4c84-bb9a-be6361e464c7)


•	Click the search bar below it and select the internet gateway you create previously. After that, click on ‘Save changes.’
![23](https://github.com/user-attachments/assets/36c277e7-5912-4e57-be85-0f1cd827d4ae)


Now, the route table will have an Internet Gateway connected to the Internet.
![24](https://github.com/user-attachments/assets/6ebaff79-5d96-45e9-bad6-e98e6f3d6ac2)



## EC2 Instances

We’ll be creating 2 EC2 instances to test our load balancer configuration.

•	On the search bar, search for EC2 and click EC2 instance.
![25](https://github.com/user-attachments/assets/4f1cd0a4-63f2-41d8-9b03-b9142536bf2c)


•	On the EC2 instance dashboard, click on launch instance.
![26](https://github.com/user-attachments/assets/155e99f0-0c06-4f4d-8582-7646bfd32605)

•	Fill in and name for your EC2 instance
![27](https://github.com/user-attachments/assets/38ea6a70-4023-41c4-a681-4c2f892e167e)


•	Leave these settings as is.
![28](https://github.com/user-attachments/assets/43e2b745-3862-44d2-a56b-05d6b73617cd)


•	Click ‘create a new key pair’ and Fill in a name for it.
![29](https://github.com/user-attachments/assets/ad41edf8-9250-4a9b-8f8b-74440105af36)
![30](https://github.com/user-attachments/assets/61d01ec4-0823-47cc-b415-8af77879621a)


•	On the network setting section, click on ‘Edit’
![31](https://github.com/user-attachments/assets/a8a37b14-e7cf-41b3-b971-e78465d13c7c)


o	Fill in the VPC we’ve been working with
o	Select the first subnet created earlier, ‘ce-class-subnet-1a’
o	‘Enable’ auto assign IP
![32](https://github.com/user-attachments/assets/bab78420-99f8-4373-9442-004015d86e24)


•	In the Firewall (security groups) section: 
o	Select ‘create secutity group’,
o	Fill in your security group name
o	Click on ‘add security group rule’
![33](https://github.com/user-attachments/assets/344f324e-8704-408a-8311-2fd77d8c3842)

o	On the ‘Type’ drop-down, select ‘http’
o	On the ‘Source type’ drop-down, select ‘Anywhere’
o	Click on the ‘Launch instance’ button
![34](https://github.com/user-attachments/assets/3ef9c3bb-2855-4fc0-81ac-0989605256ab)



•	While the EC2 instance is still initializing, create the 2nd EC2 instance following the same steps as before save for a few changes.
Use the photos as a guide to configure the 2nd EC2 instance.
![35](https://github.com/user-attachments/assets/a956fc7e-e372-48d5-aa39-dea16e4a05da)
![36](https://github.com/user-attachments/assets/150bed80-7079-4267-8f21-c362ed02e430)
![37](https://github.com/user-attachments/assets/83787240-6e52-4710-80a4-eb00f02186e9)



•	Here are the 2 EC2 instances. 
![38](https://github.com/user-attachments/assets/8c6bec03-9fd6-492c-80f6-cc6869478e0d)

The next step is to upload the web pages into the respective EC2 instances. To learn how to do so, click this link: https://github.com/tersooumah/ec2-web-hosting and follow the steps after creating the instances. 


## Target Groups
•	On the left pane of the EC2 dashboard, click on ‘Target groups’ and then ‘Create target groups’. 
![39](https://github.com/user-attachments/assets/ed43059d-0856-4252-ab2e-a7b6142468fa)


•	On the ‘Choose a target type’ section, select ‘Instances.’
![40](https://github.com/user-attachments/assets/0a46bfc2-179b-4f6d-b3f2-e8d723bb5de1)


•	Next, fill in your target group name, IP address type as IPv4, and for the VPC, select the VPC you’ve been working with and click ‘next.’
![41](https://github.com/user-attachments/assets/986f265a-b0e7-4c07-9851-a871ead9f148)


•	On the Registered tabs section, select the 2 instances we created and click ‘Include as pending below.’
![42](https://github.com/user-attachments/assets/2744bf6d-af92-4020-876e-ca5350af0e9e)

•	Click ‘Create target group’
![43](https://github.com/user-attachments/assets/446c7e39-f35b-41d7-9d16-1663ed08ee53)
![44](https://github.com/user-attachments/assets/98808ff6-e61f-4137-b793-3fa1055b0e49)



## Load Balancers
•	On the left pane of the EC2 dashboard, click on ‘Load Balancers’ and then ‘Create Load Balancer’
![46](https://github.com/user-attachments/assets/e37266e3-82a9-46a7-b07f-ed860934cbde)


•	Select Application Load Balancer by clicking create
![47](https://github.com/user-attachments/assets/88d27059-6111-4762-b73e-205cb7dde0d5)


•	Under basic configuration
o	Fill in a name for your load balancer
o	On the ‘scheme’ section Fill in ‘Internet-facing’
o	On the ‘Load balancer IP address’ type, select ‘IPv4’
![48](https://github.com/user-attachments/assets/217b53d2-9f81-4eaa-a4ea-874eed0c071b)


•	Under the security group section, click ‘create security group’
![49](https://github.com/user-attachments/assets/631146a0-3aea-47bc-a9a9-107275400233)


o	Fill in your security group name
o	Fill in a description
o	Click the VPC drop-down and select the VPC you’ve been working with.
![50](https://github.com/user-attachments/assets/3fbe11e7-aeee-45b1-a3ee-0a459ffa2115)


•	In the ‘Inbound rules’ section, click on the ‘add rule’ button.
![51](https://github.com/user-attachments/assets/763abecc-c173-4154-8df4-e74fa3b583b4)


•	In the ‘type’ column, select ‘HTTP’ in the source, select ‘Anywhere IPv4’
![52](https://github.com/user-attachments/assets/115ac6ef-21be-41fb-b433-6699367ddb1d)



•	Click on ‘create security group’
![53](https://github.com/user-attachments/assets/657e9a64-82ae-411b-ac9e-dcabd491e615)
![54](https://github.com/user-attachments/assets/d2db1fa1-3ba5-4acc-bd25-85b2340d0cce)


•	Head back to the ‘load balancer’ configuration page and back to the security group section. Select the new security group you just added. Notice that one security group was already selected? Leave it as it is, as you need both security groups
![55](https://github.com/user-attachments/assets/0091803f-6934-4d41-b5b1-bbfd790b4e27)


•	In the Listeners and routing section, in the default action column, click on the drop-down menu and select the target group we created previously.
![56](https://github.com/user-attachments/assets/1185458f-6ec9-4f37-9f6c-510fd4951a1d)


•	View the configuration you just made for the load balancer.
![57](https://github.com/user-attachments/assets/78e0d7b8-1f15-4be9-9bc7-cdd28d9b0173)


•	Click ‘Create load balancer'.
![58](https://github.com/user-attachments/assets/93b6dd21-6e80-4c5f-b02e-9db11a1a4c6d)


•	You’ve successfully created and configured the Load balancer for AWS.
![59](https://github.com/user-attachments/assets/fde7ad68-bef8-4be7-b290-d2da074e2d67)

