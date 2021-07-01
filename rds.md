**RDS**

* RDS Managed advantages
    * Managed Relational Databases.
    * Provides automatic os patching
    * DB backups
    * Monitoring Dashboards
    * Read Replicas for read performance
    * Multi AZ for high availability and disaster recovery
    * Maintenance windows
    * Scaling Horizontal with Read replicas and Vertical with auto resize.
    * Cant SSH into instances
* Available _**DB engines**_
    * Postgres
    * MySQL
    * Oracle
    * Maria DB
    * Sql Server
    * AWS Aurora
* _**Backups**_
    * Daily backups enabled by default
    * 7 days retention. Can be extended to 35 days.
* _**Snapshots**_
    * Manual backups triggered by user
    * For longer retention periods and cross AZ migration
* _**Storage Autoscaling**_
    * Automatically increase storage dynamically
    * We have to set maximum storage threshold
    * Automatically scales when free space is less than 10%, low capacity is for more than 5 minutes
* _**Read Replicas**_
    * Upto 5 replicas for RDS
    * Within Az, cross AZ and cross region
    * Async replication, data is _eventually consistent_
    * Applications must update connection string to leverage read replicas
    * In general in AWS, there is network cost when data goes from 1 AZ to another. For Read replicas, we don’t have to pay that cost for cross AZ, but cost is there for cross region
* _**Multi AZ setup**_
    * Synchronous replication from master to standby server in another AZ.
    * One DNS and automatic failover
    * We can switch from single to multi AZ setup anytime. Internally AWS will create a snapshot, restores it in another AZ and makes it standby.
* _**Security**_
    * At rest encryption with AES 256
    * In flight encryption with SSL certs
    * If master is encrypted, read replicas are also encrypted.
    * TDE (Transparent data encryption) available for oracle and sql server.
    * SSL can be enforced by parameter groups
    * Usually deployed in private subnets and use inbound rules to configure who can access.
    * IAM based (for Postgres and mysql) / username/password authentication for connecting to rds is possible.
* _**Aurora**_
    * AWS proprietary cloud optimised database
    * Supports only Postgres and mysql database engines
    * Comes with high availability and scalability by default
    * 5x performance vs rds mysql and 3x performance vs rds postgres
    * Upto 15 read replicas
    * Provides a writer and reader endpoint.
    * Data is internally sharded and stored in 3 AZs as 6 copies. Quorum consistency
        * 4 copies out of 6 for writes
        * 3 out of 6 for reads
        * Self healing with peer-peer replication
    * Storage automatically increases in 10GBs upto 64TB.
    * Instantaneous fail over mechanism.
    * 20% higher cost compared to RDS.
    * Supports auto scaling for read replicas since it has a static endpoint.
    * Backtrack feature - restore data to any point in time without backups.
    * Custom endpoints - can be used to setup a subset of read replicas as custom endpoint. For example, to run analytics queries.
    * Serverless - useful for infrequently used db workloads. Pay per second - cost effective.
    * Multimaster - for immediate failover.
    * Global Aurora - for cross region. 1 primary region, upto 5 secondary regions, 16 read replicas per secondarr region.
* _**Elasticache**_
    * Solution for caching. Supports Redis and Memcached
    * Use cases
        * Cache db queries 
        * Cache user session store
    * _Redis_
        * High availability
        * Multi Az for auto failover
        * Can be setup as a cluster
        * Use Redis auth token for security
        * Gaming leaderboards - Redis sorted sets
    * _Memcached_
        * Sharded data
        * Useful for high performance
        * No high availability
