**EC2**

* **Selections**
    * _AMI_ - Amazon Machine image
    * _Operating System_ - Windows, Linux, MAC
    * _CPU, RAM_
    * _Storage_ - Network attached: EBS / EFS, local storage
    * _Network_ - Speed of network card, Public IP address
    * _Security Group_ - Firewall rules
        * Example: Open TCP port 80 for 0.0.0.0 to allow access to web server from outside world
    * _Ec2 user data_ ->
        *  Bootstrap script
        * scripts to run on first time launch of ec2 server 
        * install software 
        * runs as root user
    * Download _Key pair_ to be able to ssh into the EC2 instance
* Every time we stop and start an EC2 instance, its public ipv4 address will change.
* **Instance Types**
    * Naming Convention -> m5.2xlarge
        * M - Instance Class
        * 5 - Generation (AWS improves hardware over time)
        * 2xlarge - more the size , more the cpu and memory
    * types
        * General Purpose (t)
            * Good Balance between memory, cpu and networking
            * Good for web servers , code repos. etc
        * Compute Optimized (c)
            * Good for Batch processing, Machine Learning, Game Server, Media transcoding
        * Memory optimised (r)
            * Processing large data sets in memory
            * Cache stores, in-memory databases
        * Storage optimised (d)
            * Databases, distributed file systems
* **Security Groups**
    * By default all inbound traffic is denied and all outbound traffic is allowed
    * Can add IP addresses, CIDR blocks or other security groups
    * Classic ports
        * 22 - SSH, SFTP
        * 21 - FTP
        * 80 - HTTP
        * 443 - HTTPS
        * 3389 - RDP
* **SSH**
    * Can ssh from local machine or putty or using ec2-instance-connect
    * Need to change the permission on the pem file from 644 to 400 using chmod \
    `> chmod 400 ec2-keypair.pem`
    `> ssh -i ec2-keypair.pem ec2-user@<public-ip> `
    * EC2 instance with Amazon Linux will come with aws cli pre-installed.
    * DO NOT add your personal aws access/secret key to run cli commands from any EC2 instance. Attach roles instead to ur ec2 instance which will give it permissions.
        
* **EC2 Instance Launch Types**
    * _On Demand_ Instances
        * For reliable, short term work loads. Predictable pricing.
    * _Reserved_ Instances
        * Requires commitment for 1 to 3 years
        * Upto 75% discount on price compared to on demand instances
        * Cannot change the instance type
    * _Convertible Reserved_ Instances
        * Upto 54% discount
        * Allows to change the instance type
    * _Spot_ Instances
        * Upto 90% discount
        * Low cost instances that are not reliable. We can loose the spot instances if someone bids more for the instance.
        * Can be used for batch jobs, image processing etc.
    * _Dedicated Hosts_
        * Reserved physical server for you
        * For compliance requirements, server specific software licenses
        * Allows access to hardware internals of the server
    * _Dedicated Instances_
        * Similar to Dedicated host but does not give access to the hardware
        * Hardware can change when instances are stopped and started.
    * _EC2 Fleets_
        * Pool of spot and on demand instances that can be created based on provided config
* **Placement Groups**
    * Logical grouping of instances
    * Types
        * _Cluster_
            * All instances are placed in the same AZ, same network
            * Low latency 
            * single point of failure
        * _Spread_
            * All instances are spread and placed in different racks.
            * Can span multiple AZs, maximum of 7 instances per AZ
            * High availability 
        * _Partition_
            * Instances in each partition is placed in different racks
            * We can control instances goes to which partition
            * Used for distributed workloads like HDFC, HBase, Cassandra
* **AMI - Amazon Machine Image**
    * Like Docker image
    * Can create custom AMI out of an existing EC2 instance
    * For example, provision an ec2 instance install Apache server in it and create an AMI out of it.
