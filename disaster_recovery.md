**Disaster Recovery**

[back](index.md)

* RTO recovery time objective - accepted time to recover after a service disruption
* RPO recovery point objective - accepted hours of data loss after a service disruption
* Disaster recovery strategies
    * backup and restore
      * schedule a data backup on hourly / daily basis or use snowball once a week.
      * instances are not run in multiple zones. when disaster hits, we reactively provision instances.
      * low cost and high RTO and RPO.
    * pilot light
      * continuous replication of data to secondary region
      * a small version of app is always running in cloud
      * use route53 to route to secondary if disaster occurs
    * warm standby
      * a secondary full system is up and running but minimal scale
      * ASG can help to scale on demand
    * multisite
      * active-active mode where route53 will route traffic to multiple sites all the time
      * High cost and low RTO/RPO
    
**Database Migration Service DMS**
* Used to migrate database from on premise to aws cloud
* source db is always available during migration
* can do heterogenuous migrations from one type of source db to different type of destination db
* uses CDC change data capture via an EC2 instance
* SCT Scheme conversion tool to convert from one db engine to another engine

**On premise migration strategies**
* can use AWS linux AMIs as VMs on prem
* vm import / export
* AWS application discovery service can be used to scan and plan a migration of huge number of on prem servers.
* DMS - replication of on prem db to aws
* SMS - incremental replication of on prem servers to aws
* AWS data sync - to sync large amounts of data on prem in NFS / SMB protocols to AWS S3 / Glacier / EFS etc. can be scheduled at regular intervals.

**AWS Backup**
* managed service to create a backup plan across multiple aws services
* supports RDS, EFS, EC2 Dynamodb etc.
* supports on demand and scheduled backs and PITR (point in time recovery)


[back](index.md)