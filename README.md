#--aws-public-private-subnet-architecture
-aws-public-private-subnet-architecture
# Secure VPC Architecture with Public and Private Subnets for Production Environment
## Overview :
This project's overview is depicted in the diagram below. The setup revolves around a Virtual Private Cloud (VPC) featuring both public and private subnets, thoughtfully distributed across two Availability Zones to ensure reliability.

Within each public subnet, there's a NAT gateway to facilitate outbound internet connectivity and a load balancer node for effective traffic distribution.

On the other hand, the project's servers reside in the private subnets. Their deployment and termination are automated through an Auto Scaling group, allowing them to dynamically adapt to workload changes. These servers play a pivotal role in receiving traffic from the load balancer and can access the internet through the NAT gateway when necessary


![image](https://github.com/itz-mathesh/aws-public-private-subnet-architecture/assets/144098846/9d656294-2011-4467-a620-63954d923710)

## Steps :
### Step 1 :
#### Create the VPC :
1. Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.
2. On the dashboard, click on "Create VPC."
3. Under "Resources to create," select "VPC and more."
4. Configure the VPC:<br>
   a. Provide a name for the VPC in the "Name tag auto-generation" field.<br>
   b. For the IPv4 CIDR block, leave it as default suggestion.<br>
5. Configure the subnets:<br>
   a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.<br>
   b. Specify the "Number of public subnets" as 2.<br>
   c. Specify the "Number of private subnets" as 2.<br>
   d. For NAT gateways, choose "1 per AZ" to enhance resiliency.<br>
   g. For VPC endpoints, you can choose "None" .<br>
   h. Regarding DNS options, clear the checkbox for "Enable DNS hostnames."<br>

Once you've configured all the settings, click "Create VPC."


![vpc](https://github.com/user-attachments/assets/1633af81-e046-4bd8-a063-afd66331df51)


![2](https://github.com/user-attachments/assets/5f24cbb1-2c71-4498-adf6-d116eaad155e)

![3](https://github.com/user-attachments/assets/4169c327-f901-4419-8a66-d85e404ea087)


![4](https://github.com/user-attachments/assets/5cc58f5a-006a-4b86-a985-933ad5001627)


6. Now you can see you are successfully Created VPC .




### Step 2:
#### Creating the Auto Scaling Group :

![5](https://github.com/user-attachments/assets/c0828b57-e866-4e5a-bbaf-53ba6b6aedc9)


![6](https://github.com/user-attachments/assets/58d7614e-be12-48b2-b6a8-8cd4c48a986a)

![7](https://github.com/user-attachments/assets/9a5dd20b-26f1-46c7-a64f-226c109ab193)


![13](https://github.com/user-attachments/assets/963ba598-56f6-4d77-bee6-0c1fee679fec)



1. Now you have to choose the Key-pair you created.

![17](https://github.com/user-attachments/assets/ab4a9260-69c0-4996-a468-abed9439cc3b)


![14](https://github.com/user-attachments/assets/89f58404-4726-4668-b637-d96529e28754)



![15](https://github.com/user-attachments/assets/85b88629-9cea-4807-90cb-c5f003552bf7)

![16](https://github.com/user-attachments/assets/3cf8ff9d-4da5-4e53-99d2-c665500200fc)

![7](https://github.com/user-attachments/assets/75efc4e1-fbcf-42bf-9a6b-b97e71d74fa1)


2. Scroll Down and then Click "Next".
![8](https://github.com/user-attachments/assets/4b3d0b41-fb65-43cd-b689-2de67e0c1895)


3. Scroll Down and then Click "Next".

![9](https://github.com/user-attachments/assets/05f80eb4-9f8b-46a8-af61-efe26f05b772)


4. Scroll Down and then Click "Next".

![10](https://github.com/user-attachments/assets/c97b544f-2c82-4bdf-8545-db0ebb1cec2b)


5. Scroll Down and then Click "Skip to Review".

![11](https://github.com/user-attachments/assets/d8b5e021-6ec7-45e9-905e-6f27165f318d)

6. Now your are Successfully Created Auto Scaling Group.<br>
7. Open the AWS Management Console.<br>
8. Navigate to the EC2 console by clicking on "Services" in the top-left corner, then selecting "EC2" under the "Compute" section.<br>
9. In the EC2 dashboard, you'll find the "Instances" link on the left-hand navigation pane. Click on "Instances."<br>
10. Here, you should see the list of EC2 instances associated with your account. Look for the instances created by your Auto Scaling Group.<br>
Since you mentioned that the Auto Scaling Group launched instances in different AZs, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple AZs.

### Step 3 :
#### Creating the Bastion Host :

1. Launch Instance as Specified below .

![19](https://github.com/user-attachments/assets/44a6a6e1-2394-4317-9351-a7e93890714b)


![20](https://github.com/user-attachments/assets/988946b1-8400-45a6-a20e-bc5238493a05)


![21](https://github.com/user-attachments/assets/f14ee2cc-735f-4822-a1ce-8694e86f1a0f)


![22](https://github.com/user-attachments/assets/3e2c5fa2-79ef-4102-b5a9-0df82d74882c)



![18](https://github.com/user-attachments/assets/33e8a0f9-c32d-4f45-b8df-c1872b753b6c)



### Step 4: 
#### SSH into Private Instance

1. SSH into the Bastion Host Instance:
   To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we'll be able to SSH into the private instance.
2. Ensure the PEM File is Present on the Bastion Host:
   Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won't be able to SSH into the private instance from the Bastion host.
3. Open a Terminal:
   Open a terminal window on your local machine.
4. Execute the Following Commands:
   a. If your PEM file is named something like `<aws demo.pem>`, you must remove spaces in the filename. Please rename the file to something like `<aws_demo.pem>`.
   b. Copy the PEM file to the Bastion host using the `scp` command. Replace `<pem file location>` with the local and remote file paths, and `<bastion host public IP>` with the Bastion host's public IP address. 
   Example:
      ```
      scp -i /Users/mathesh/Downloads/aws_demo.pem /Users/mathesh/Downloads/aws_demo.pem ubuntu@34.229.240.123:/home/ubuntu
      ```
   c. The above command will copy the PEM file from your computer to the Bastion host. Once the file is successfully copied, move on to the next step.
   d. SSH into the Bastion host using the following command:
      ```
      ssh -i aws_demo.pem ubuntu@34.229.240.123
      ```
    e. After SSHing into the Bastion host, use the `ls` command to check if the `aws_demo.pem` file is present. If it's not there, double-check your previous commands.
    f. Now, you can SSH into the private instance using the following command, replacing `<private IP>` with the private instance's IP address:
      ```
      ssh -i aws_demo.pem ubuntu@<private IP>
      ```
    g. We will deploy our application on one of the private instances to test the load balancer.
    h. After successfully SSHing into the private instance, create an HTML file using the Vim text editor:
      ```
      vim demo.html
      ```
    i. This will open the Vim editor. Copy and paste any HTML content you like into the editor.
    j. For example:
      ```html
      <!DOCTYPE html>
      <html>
      <head>
      <title>Page Title</title>
      </head>
      <body>

      <h1>This is an AWS Demo Production</h1>
      </body>
      </html>
      ```
     k. After pasting the content, save the file by pressing 'Esc' to exit insert mode and then entering `:w` to save.
     l. Finally, start a Python HTTP server on port 8000 to deploy your application on the private instance:
      ```
      python3 -m http.server 8000
      ```
Now, your application is deployed on the private instance on port 8000.
### Note :
We intentionally deployed the application on only one instance to check if the Load Balancer will distribute 50% of the traffic to one instance (which will receive a response) and 50% to another instance (which will not receive a response).

### Step 4 :
#### Creating the Load Balancer :

1. Access the EC2 Terminal.
2. Follow the steps outlined below.

![24](https://github.com/user-attachments/assets/82f6a941-4e83-44fd-b9ea-6f6c5dcab50a)


![25](https://github.com/user-attachments/assets/adc94e0b-c2b9-490c-8451-3424d7e1a0f2)


![26](https://github.com/user-attachments/assets/34a1ce12-1e7b-45fd-93e4-d40d965e52d1)


![27](https://github.com/user-attachments/assets/397af7de-aba2-410e-8455-54778179985d)


![28](https://github.com/user-attachments/assets/be22918a-0019-4ffa-b31a-4ce34827b2c2)


![29](https://github.com/user-attachments/assets/eb59c5b8-bc5d-47b3-86cf-781af0ae89e5)


![30](https://github.com/user-attachments/assets/a888554a-f7c8-4c3c-90e6-782bd02772bb)

![31](https://github.com/user-attachments/assets/1e9376a5-d1de-43e6-8940-60e27361adf4)


![23](https://github.com/user-attachments/assets/710fc175-3ec1-4a1e-a9b9-efcd20dff47a)



Now We Successfully deployed Application securely in Private instance , We can access it through Internet using Load Balancer Securely .
