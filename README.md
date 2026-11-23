# AWS-LOAD-BALANCER
# EX 6B AWS LOAD BALANCER
## NAME:Mopuri Saradeepika
## REG NUMBER: 212224040201
## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.
### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT
<img width="1920" height="1200" alt="Screenshot (152)" src="https://github.com/user-attachments/assets/62ba26e5-3080-4b7c-bb1b-b2339f919e7d" />

<img width="1920" height="1200" alt="Screenshot (153)" src="https://github.com/user-attachments/assets/17ac62db-8ff9-44ff-977c-b233f70a54e8" />

<img width="1920" height="1200" alt="Screenshot (154)" src="https://github.com/user-attachments/assets/6ef5ef11-04ac-4fc7-a24a-f6ec91bc3ba1" />

<img width="1920" height="1200" alt="Screenshot (155)" src="https://github.com/user-attachments/assets/ea18c1b8-065b-4264-94c3-db32e379956c" />

<img width="1920" height="1200" alt="Screenshot (156)" src="https://github.com/user-attachments/assets/e1e078e3-23be-4544-84bd-d97f6eae415b" />

<img width="1920" height="1200" alt="Screenshot (157)" src="https://github.com/user-attachments/assets/ccf70da2-b73b-48bd-b69e-ce1d1514a995" />

<img width="1920" height="1200" alt="Screenshot (158)" src="https://github.com/user-attachments/assets/08285f1e-b4f7-489c-bb26-dac4b526bf51" />

<img width="1920" height="1200" alt="Screenshot (160)" src="https://github.com/user-attachments/assets/74a37a81-8dbd-46c9-a89b-27da872ac2cb" />

<img width="1920" height="1200" alt="Screenshot (162)" src="https://github.com/user-attachments/assets/bec25c3b-e6c3-419e-bbcc-08b1f73e915f" />

<img width="1920" height="1200" alt="Screenshot (163)" src="https://github.com/user-attachments/assets/66127482-deff-4479-8c80-80018030907d" />

<img width="1920" height="1200" alt="Screenshot (165)" src="https://github.com/user-attachments/assets/ea9b3c93-42a9-4671-a767-d3bafc5e2c45" />

<img width="1920" height="1200" alt="Screenshot (167)" src="https://github.com/user-attachments/assets/a9f99688-1c2e-4a94-a966-381e6908bd58" />

<img width="1920" height="1200" alt="Screenshot (168)" src="https://github.com/user-attachments/assets/73b4f919-f69b-4924-9065-461aba0ffd8d" />

<img width="1920" height="1200" alt="Screenshot (170)" src="https://github.com/user-attachments/assets/ad45fa52-dc86-446a-a43b-f411c6b6ecb5" />

<img width="1920" height="1200" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/e5c1bf33-f303-4e09-a93f-7ce5684e4fd7" />

<img width="1920" height="1200" alt="Screenshot (173)" src="https://github.com/user-attachments/assets/9680ec73-a580-47a6-9d9e-9f81bacf98ab" />

<img width="950" height="436" alt="image" src="https://github.com/user-attachments/assets/4c0e3cb4-5c20-4847-b8b9-4714259f8c5c" />

## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
