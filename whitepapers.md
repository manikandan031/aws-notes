**White Papers**

[back](index.md)

* Well Architected Framework (5 pillars)
    * Operational effectiveness
        * Infrastructure as code
        * AWS config to validate compliance of Cloud Formation
        * small frequent changes - CI & CD
        * anticipate failure and learn from failures
    * Security
        * least priviege
        * enable traceability
        * Security at each layer - Edge network, VPC, subnet, ALBs, security groups
        * security in transit - encryption, temp. credentials, MFA
        * Shield, WAF, inspector to secure infrastructure
    * Reliability
        * automatically recover from failure
        * simulate and test failures
        * use autoscaling, dont guess capacity
        * AWS Service quotas, trusted advisor
    * Performance
        * use serverless architectures
        * should be able to deploy global in minutes
        * lambda, ASGs, S3, RDS, CF, Elasticache
    * Cost optimization
        * AWS Budgets, AWS cost explorer
        * reserved instances, spot instances
        * glacier for cold storage
        * autoscaling & lambdas
* AWS well architected tool - to learn, and measure architectural best practices.
    * can define a workload
    * asks questions on the above 5 pillars and generates report
* AWS Trusted advisor
    * analyse your aws account on the 5 pillars and provides recommendations.
    * weekly email notifications
* More AWS Architectures
    * https://aws.amazon.com/architecture
    * https://aws.amazon.com/solutions
    * https://aws.amazon.com/whitepapers
        * Architecting for the cloud: AWS best practices
        * AWS Well architected framework
        * AWS disaster recovery - https://aws.amazon.com/disaster-recovery



[back](index.md)