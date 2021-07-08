**Snow Family**

[back](index.md)

* Used to migrate large volumes of data into AWS servers. 100s of TBs / PBs of data can be transferred. Uploading these over the network can be ineffiecient and expensive. Also used to process data at the edge and process. (Edge computing).
* AWS will send a physical storage device to our address and we need to upload / download data from it.
* AWS Snow cone, Snowball edge, Snowmobile - Data migration
* AWS Snow cone, Snowball edge - Edge computing
* **Snow Cone** 
    * Small portable device that can withstand harsh environments
    * Can store upto 8TBs of data
    * Can sync data using AWS data sync when the device is online or can be shipped to AWS offline
* **Snowball edge**
    * Larger device. Can store 80TBs of data.
    * Storage optimized - 80TBs
    * Compute optimized - 42 TBs
* **Snowmobile**
    * Much larger device ( like a truck)
    * 1 snowmobile Can store upto 100 PBs of data. Can be used to transfer Exa bytes of data.
    * Has additional security like GPS, 24x7 video surveillance etc
* Snowball edge / Snowcone - can be used for edge computing while offline and then ship back the data.
* AwsOpshub - can be used to work with snow family devices.
* Import data from snowball into S3 and then use lifecycle policy to load data into glacier.

**Exposing S3 data to On Prem**
* Storage gateway
    * File gateway - To allow access to S3 via smb protocol / nfs . File gateway is mounted on Prem. Integrated with Active Directory.
    * Volume gateway - to backup application storage in S3 as EBS snapshots. 
    * Tape Gateway - Physical tapes used to back up data. Stored as virtual tapes in S3.
* Storage Gateway Hardware Appliance can be purchase from amazon and used to access these gateways

**Amazon Fsx for windows**
* EFS is only for Linux
* Amazon Fsx is a scalable network storage like EFS for windows
* Daily backups in S3

**Amazon Fsx for Lustre**
* Large scale computing,  machine learning, HPC (High performance computing) in linux
* Scales upto 100s of GBs per second
* Scratch file system and Persistent File system

**AWS Transfer Family**
* To transfer files in or out of s3 using ftp protocols
* FTP, FTPS, SFTP
* Integrates with existing auth mechanisms

[back](index.md)
