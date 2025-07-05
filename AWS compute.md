
---

Server hosts an application. Client is a person/ computer that sends a request. Servers provide us CPU memory and network capacity. On AWS to run a http server find a service that provides a compute power. 

Eg: EC2 , Lambda etc.

### Three fundamental services:

1. VMs - Instances of Compute -> Provides physical server. EC2
2. Containers - 
3. Serverless

### EC2:

Creation of an EC2 instance can be done through console , CLI or SDks, automation tools and infra services.
Following must defined to call an EC2 instance:

1. Hardware specs: cpu , mem and storage.
2. Logical: Networking location, firewall rules and OS.

#### AMI amazon machine image:

It contains the image of an OS. This OS will be installed on your instance.
Relationship between AMI and EC2: Its like class and object.

Amazon provides AMI there are custom and community AMI also. Each ami has ami id:  format-> ami-hash

EC2 has many instance types - they define the cpu , memory , network of VM. They have specific name and carry some meaning 

Format : instance family generation   attribute .  Instance size -> c5n.xlarge

Instance families:

	1. General purpose - for web server 
	2. Compute optimised - 
	3. Memory optimised
	4. Storage optimised

#### EC2 instance locations:

By default Ec2 instances are placed in default virtual private cloud(vpc). Any resource put inside here is accessible by internet. One can also choose custom vpc and with restricted access.


#### EC2 lifecycle:

![[Pasted image 20250705125316.png]]


1. When launched -> pending state. Here its preparing to enter running stage.
2. Running -> ready to use. BIlling starts. 
3. Rebooting -> Rebooting OS. Instance keeps its IPv4 and IPv6 address.
4. Stopping and stopped -> Shut down. Keeps IPv4 and IPv6
5. Terminate -> Instance stored is erased and loose IPs

Stop and stop hibernate: In stop ram data is lost but in hibernate its stored in ebs volume.




