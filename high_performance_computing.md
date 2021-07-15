**HPC High Performance Computing & High Availability**

[back](index.md)

**HPC**
* Data Transfer
  * Direct Connect - hundreds of GBs of data over a private secure network
  * Snowball & Snowmobile - to transfer Petabytes of data into aws
  * AWS data sync - to load large amounts of data from on prem to aws. can work with direct connect to transfer via private network.
* Compute & Networking
  * EC2 instance types can be selected accordingly for compute optimized workloads.
  * Spot instances can be used for cost benefits.
  * EC2 fleets with Cluster placement group can be used to reduce network latency since they wil be in same rack.
  * EC2 enhanced networking ENA can be used to get even higher network performance
  * EFA Elastic fabric adapter gives even higher performance by bypassing the underlying linux OS.
* Storage
  * Instance local storage
    * EBS - 64000 Iops
    * EC2 Instance Store - millions of IOPs
  * Network Storage
    * S3 large blob storage
    * EFS - scale IOPs based on provisioned size
    * Amazon Fsx for Lustre - backed by S3
* Automation and Orchestration
    * AWS Batch - to run multinode parallel jobs. easily launch ec2 instances.
    * AWS parallel cluster - open source cluster mgmt tool to deploy HPC on AWS.


**HA**

* EC2 
    * use CW event + Lambda to provision new ec2 instance and point the elastic ip to the new instance
    * use EC2 user data script to assign the elastic ip to that instance. this setting with ASG (min 1 and max 1) .
* Bastion Host
    * Use NLB and have multiple bastion hosts.

[back](index.md)