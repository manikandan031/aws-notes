**VPC**

[back](index.md)

* CIDR blocks represent a range of IPs. ex. 0.0.0.0/0
* Private IPs - 10.x.x.x, 172.16.x.x, 192.168.x.x
* 10.0.0.0/16 -> 10.0.0.0 - 10.0.255.255 - 65536 ips. It means last 16 out of the 32 bits can change.
* Default VPC comes with 3 subnets, 1 route table, 1 IGW, 1 Network ACL
* Default VPC gives instances public and private DNS names.
* A VPC can have upto 5 CIDR block IP ranges. Minimum size /28 = 2 ^ (32-28) = 16 IPs of which 5 will be reserved for internal use.
* 5 internal use IPs for 10.0.0.0/16
  * 10.0.0.0 - network address
  * 10.0.0.1 - address for vpc router
  * 10.0.0.2 - aws provided dns service
  * 10.0.0.3 - reserved for future use
  * 10.0.255.255 - network broadcast address (last IP of CIDR)
    
    
**Subnets & Internet Gateways**
* Subnets are smaller blocks of IP ranges within a VPC. They are AZ specific.
* Subnets can be made public by attaching a IGW to the VPC and updating the route table with the subnet association to route all traffic to the IGW.
* Public subnets are usually smaller because we only put our Load balancers in it
* Private subnets are larger as we put all our application stuff in it
* 1 IGW per VPC
* Ex. 
    * VPC - 10.0.0.0/16 (10.0.0.0 - 10.0.255.255 65536 IPs)
    * Public Subnet 1  - 10.0.0.0/24 (10.0.0.0 - 10.0.0.255 256 IPs) AZ1
    * Public subnet 2  - 10.0.1.0/24 (10.0.1.0 - 10.0.1.255 256 IPs) AZ2
    * Private subnet 1 - 10.0.16.0/20 (10.0.16.0 - 10.0.31.255 4096 IPs) AZ1
    * Private subnet 2 - 10.0.32.0/20 (10.0.32.0 - 10.0.63.255 4096 IPs) AZ1
    * Go to VPC Route tables. create a new route table and associate the public subnets with it.
    * Add a route for traffic from 0.0.0.0/0 to IGW. This will give internet access to the public subnet and also the instances can be accessed from internet.
    
**NAT instances and NAT Gateways**
* NAT instances are old way of doing things. NAT gateway is the recommended way.
* NAT allows to give internet access from private subnet without exposing the private subnet to access from internet.
* NAT instance
  * create a ec2 instance with NAT AMI and run it in public subnet. This will be the nat instance.
  * create a route table in the VPC and associate the private subnets.
  * add a route to route all traffic to NAT instance. Since NAT instance is connected to IGW now private subnet gets internet access.
  * Need to update the NAT instance security groups to allow incoming traffic from within VPC on specific ports.
* NAT gateway
  * NAT Gateway is at AZ level. Need to create a NAT Gateway for each AZ for reseliency.
  * NAT gateway is created in the public subnet. It needs a elastic IP.
  * Add a route in the private subnet to route all traffic to NAT gateway.
    
**DNS Resolution Settings**
* enableDNSSupport - True (Default) if AWS DNS resolution is enabled.If True queries 169.254.169.253 aws dns server.
* enableDNSHostName - If enabled a DNS host name is auto assigned if there is a public IP. For Default VPC this is True by default for other VPC false by default.
* To use customer domain names within VPC in a private Hosted Zone in Route 53, we must enable both these.

**Network ACL and Security Groups**
* Network ACL are rules at subnet level and security groups are rules at instance level within subnet.
* Security group rules are stateful - for incoming request, if request is allowed to come in then it will not check the outbound rules.
* Network ACL rules are stateless - should allow in both inbound and outbound rules.
* Network ACL rules are numbered. lower numbers take higher precedence.
* Default Network ACL has a rule to allow all traffic. New Network ACL will block all traffic. we need to set up rules to allow traffic.

**VPC Peering**
* Allow 2 VPC to connect in private AWS network.
* the subnets must not be overlapping.
* VPC peering connection is not transitive.
* We can de VPC peering across accounts and across region.
* must update route tables of public subnets of both VPCs to route traffic to the other VPC CIDR to the VPC peering connection.

**VPC Endpoints**
* To access AWS managed services from instances via private network without going via internet.
* Remove the NAT gateway route from your VPC route table to cut off internet access for private subnet.
* Create a VPC endpoint pointing to the target service - S3 / Dynamodb / RDS etc.
* Add a route in the private subnet route table to route traffic to S3 CIDR / hostnames to the VPC endpoint.

**VPC Flow Logs**
* Flow logs can be used to track requests / traffic - source and dest. IPs whether it was accepted / rejected etc.
* Flow logs can be sent to Cloud watch or S3. If sent to S3 it can be analysed via Athena.

**Bastion Hosts**
* Typically instances in private subnet can be SSHed into only from an instance in the public subnet.
* This instance in the public subnet is called the Bastion host. 
* We need to use the pem file for the private subnet instance while SSHing from the bastion host.

**Site to site VPN, Virtual Private Gateway and Customer Gateway**
* Used to set up a VPN connection from corporate Data center to a single AWS VPC.
* traffic goes through internet but its encrypted.

**Direct Connect & Direct Connect Gateway**
* used to set up a private connection from corporate data center to aws vpc using a aws direct connect location
* takes around a month to set up
* can connect multiple VPCs to the direct connect gateway
* data is not encrypted since it is a private network. can use VPN for encryption on top.

**Egress only Internet Gateway**
* NAT gateway For IPV6 instances.

**AWS Private Link / VPC endpoint services**
* Used to share a specific service in one VPC to other VPCs (even 1000s of VPCs)
* a NLB is set up in front of the service to be exposed.
* An ENI is set up on the consumer VPC and the ENI and NLB are linked privately.

**AWS classic Link (Deprecated)**
* EC2 classic - old types of ec2 instances which run in single network shared with other customers (before VPC world)
* to connect EC2 classic instances to VPC we can use AWS classic link

**VPN cloud hub**
* to connect multiple on premise sites together along with aws vpc.

**Transit gateway**
* a transit gateway is like a mediator to which we can connect multiple VPCs, site-to-site vpn, direct connect gateway etc.
* hub and spoke (star) connection pattern.
* regional resource but we can peer transit gateways across regions.
* supports IP multicast
* ECMP equal cost multi path routing can be used to increase the bandwidth of the vpn connections

**IPV6 for VPC**
* Even when we use IPV6 for instance in your VPC, it still assigns a private IPV4 address to your instance.
* So if we run out of IPV4 address you cannot add instances without adding a new CIDR into your private subnet.


[back](index.md)