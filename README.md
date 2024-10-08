# AWS-networking-VPC-1

<img width="683" alt="Screenshot 2024-09-03 at 2 07 28 AM" src="https://github.com/user-attachments/assets/a0940e53-f6c3-49aa-960d-0cdb637a93bf">

AWS VPC Network Architecture Overview
This diagram represents a common network setup in Amazon Web Services (AWS) using a Virtual Private Cloud (VPC). The architecture includes both public and private subnets, an Internet Gateway, route tables, and EC2 instances.

Key Components:
VPC (Virtual Private Cloud):

The VPC is the overarching network environment in AWS, providing isolated virtual networks where you can launch AWS resources.
The entire VPC has a CIDR block of 12.0.0.0/16, which is divided into smaller subnets.
Subnets:

Public Subnet (12.0.1.0/24):
This subnet is accessible from the internet. It is typically used to host public-facing resources like web servers (EC2 instances) that need to communicate directly with the outside world.
Private Subnet (12.0.2.0/24):
This subnet is isolated from the internet and is generally used for backend resources such as databases (EC2 instances) that should not be exposed publicly.
EC2 Instances:

EC2 in Public Subnet:
This instance is deployed in the public subnet, which has direct access to the internet via the Internet Gateway.
EC2 in Private Subnet:
This instance is deployed in the private subnet and does not have direct internet access. It can communicate with the EC2 in the public subnet.
Internet Gateway:

The Internet Gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
It is attached to the VPC to enable internet access for instances in the public subnet.
Route Table:

Route tables contain a set of rules (routes) that determine where network traffic is directed.
The route table in this diagram directs traffic from the subnets:
The public subnet routes traffic to the Internet Gateway, allowing the EC2 instance in this subnet to communicate with the internet.
The private subnet can route traffic through the EC2 instance in the public subnet (acting as a bastion host or NAT instance) or directly to another private subnet.
CIDR Blocks:

The CIDR notation (Classless Inter-Domain Routing) defines the IP address range of the VPC, subnets, and route destinations.
In this example, 12.0.0.0/16 is the VPC range, with 12.0.1.0/24 and 12.0.2.0/24 as the respective subnet ranges.
Network Traffic Flow:
Internet Access:

The EC2 instance in the public subnet can send and receive traffic to/from the internet through the Internet Gateway.
The EC2 instance in the private subnet cannot directly access the internet but can communicate with the public EC2 instance, which might act as a proxy.
Inter-Subnet Communication:

The EC2 instance in the public subnet can communicate directly with the EC2 instance in the private subnet, allowing for secure, internal-only communication between these instances.
Use Cases:
Public Subnet: Host public-facing applications, web servers, or bastion hosts.
Private Subnet: Host backend services like databases, caches, or internal application servers that should not be directly accessible from the internet.
This architecture ensures a clear separation between public and private resources, enhancing security while allowing necessary access and communication.


<img width="683" alt="Screenshot 2024-09-03 at 2 07 28 AM" src="https://github.com/user-attachments/assets/a0940e53-f6c3-49aa-960d-0cdb637a93bf">


we are going to configure our vpc acccording to above image 

We Need 4 steps 

1. Create Vpc
2. create internet gateway
3. Create subnet
4. create route table
5. create EC2 instances

and configure according to the above image .

Create VPC 

need to give name and cidr range in my case i have given 12.0.0.0/16

<img width="985" alt="Screenshot 2024-09-03 at 2 13 12 AM" src="https://github.com/user-attachments/assets/0aa2868f-fc40-499b-bfa3-77c327c05b63">
<img width="985" alt="Screenshot 2024-09-03 at 2 13 23 AM" src="https://github.com/user-attachments/assets/f73dc77c-6b51-4ff9-ae7c-99b86b318d35">

create internet gateway

Go to internet gateway in left  hand side in aws portal.

Click on create gateway by giving name 

Need to attach to vpc click ---> goto action -->click on attach gateway


<img width="1429" alt="Screenshot 2024-09-03 at 2 25 30 AM" src="https://github.com/user-attachments/assets/df7b6fae-974f-4bde-8e1c-891a2d3d3205">

create Subnet

Go to subnets in left  hand side in aws portal.

create private subnet

<img width="1429" alt="Screenshot 2024-09-03 at 2 30 44 AM" src="https://github.com/user-attachments/assets/5eb06f03-dea5-4a7f-a375-8e9b9a48cc35">


create public subnet

<img width="1429" alt="Screenshot 2024-09-03 at 2 31 45 AM" src="https://github.com/user-attachments/assets/79963729-7c59-4c3a-a325-12112d866b14">

Create route table 

<img width="1429" alt="Screenshot 2024-09-03 at 2 37 16 AM" src="https://github.com/user-attachments/assets/ddc96630-f916-489f-91a6-b6964231c5f7">

we need to provide the route to access the internet 

click on route id then click on edit route 

click on add route  and add internet gateway.

<img width="1429" alt="Screenshot 2024-09-03 at 2 41 07 AM" src="https://github.com/user-attachments/assets/5204a7cf-f274-4938-a695-e61341260929">


<img width="1429" alt="Screenshot 2024-09-03 at 2 42 34 AM" src="https://github.com/user-attachments/assets/622d450d-6c04-4d30-bb75-f3e2ade1ca5e">



We need to associate the subnet to route table public 

In public route table click on the SUBNET ASSOCIATION ---> edit subnet association ---> add subnet listed 

<img width="1429" alt="Screenshot 2024-09-03 at 2 49 47 AM" src="https://github.com/user-attachments/assets/e2769dd3-a667-40b5-8b7d-c78614559df0">

follow same create route table as public and dont add internet gateway which we dont require for private 


We need to associate the subnet to route table private

In public route table click on the SUBNET ASSOCIATION ---> edit subnet association ---> add subnet listed 

<img width="1429" alt="Screenshot 2024-09-03 at 2 53 47 AM" src="https://github.com/user-attachments/assets/e6b1b764-8c0a-499d-a660-4deb9530c84e">

NOW CREATE THE RESOURCES INSIDE THE PRIVATE AND PUBLIC SUBNET (EC2 INSTANCES )

<img width="1429" alt="Screenshot 2024-09-03 at 2 59 33 AM" src="https://github.com/user-attachments/assets/e39656f3-88ef-4af9-b62a-660ac4de92b7">

<img width="1046" alt="Screenshot 2024-09-03 at 3 07 22 AM" src="https://github.com/user-attachments/assets/4d475036-43e1-4894-9d8d-54d555b2279f">

NOTE : After this practice kindly delete the all resources to avoid the cost .









