**EBS and EFS**

[back](index.md)

* **EBS** - Elastic Block Store
    * Network file storage
    * Local to a AZ
    * Can be easily attached and detached to Ec2 instances
    * Each EC2 instance has a default root volume
    * _Delete on termination_ - deletes volume on EC2 instance stop.
    * _Snapshots_ - Backup of EBS volumes
        * Can be used to port volumes across AZ
    * Volume Types
        * _Gp2/gp3_
            *  General Purpose volumes
            * Balance price and performance
            * 1GB - 16TB
            * Upto 16000 IOPS (IO operations per sec)
        * _Io1/io2_
            * High performance volumes
            * Low latency and high throughput workloads
            * Great for Database workloads
            * More than 16000 IOPs
            * 4GB - 16TB
            * EC2 Nitron instances - 64000 IOPS
            * Io2 block express - max tops 256000 IOPS, 64 TB
        * _St1_
            * Low cost volumes
            * Throughput intense workloads
            * Big Data, Data Warehouse
        * _Sc1_
            * Lowest cost volumes
            * Low throughput
            * Cold storage - infrequent access
    * EBS volumes can be encrypted
    * _RAID_
        * OS Level setting to optimise storage performance or increase availability
        * EBS is already redundant within AZ
        * We can use RAID settings if we want to increase redundancy further or increase IOPs
        * _RAID0_
            * Optimise performance
            * 1 logical volume in front of 2 or more EBS volumes and data block is stored in either 1 of the volumes
        * _RAID1_
            * Increase availability / fault tolerance
            * 1 logical volume in front of 2 or more EBS volumes and data blocks are stores in all of them for redundancy.
* **EFS - Elastic File System**
    * Network storage
    * Not tied to Availability Zone
    * 3 times expensive than gp2 EBS
    * Pay for what you use, no capacity planning
    * Same EFS can be mounted to multiple EC2 instances in multiple AZs
    * Use cases - Word Press, Content Management System, Data sharing
    * _POSIX_ file system, works only with Linux
    * Can store Petabytes of data
    * Performance mode
        * General Purpose - Low latency. Useful for web serving
        * Max I/O - High Latency, High throughput. Useful for Bigdata
    * Throughput mode
        * Bursting
            * Provisioned - if we want high thoughput with a low volume
    * Storage Tiers
        * Move files to infrequent access after n days. Reduces cost.
* **EC2 Instance Store**
    * Local storage for the EC2 instance
    * Will be lost If the EC2 instance is stopped
    * Provides very low latency since its local.

[back](index.md)
