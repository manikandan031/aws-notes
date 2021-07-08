**Route 53 and Elastic Bean stalk**

[back](index.md)

**Route 53**
* DNS registrar and DNS system
* Route 53 can also be used along with external DNS registrar like GoDaddy
    * We need to create a public hosted zone in AWS Route 53
    * Update the Name Server records displayed in AWS in the external DNS service
* DNS format -> _app_._domain_.com
* CNAME records -
    *  hostname to hostname mapping
    * Cannot be used for root domain
* A records
    * Hostname to ip address
* Alias records
    * Hostname to target AWS resource like Load balancer
* Routing Policy
    * Simple - Single host name to Single resource / Load balancer
    * Failover - active-passive failover
    * Weighted - route to different targets based on weight specified
    * Latency - route traffic based on latency
    * GeoLocation - route traffic based on user location
    * GeoProximity - similar to geo location but we can sepcify a bias to shift more traffic to one location
    * MultiValue - responds with multiple records for client side load balancing

**Elastic Beanstalk**
* Combination of Golden AMI and Ec2 user data. 
* Managed service to easily deploy and scale web applications. 
* Takes care of capacity provisioning, load balancing, auto scaling 
* Options
    * Single instance deployment - non prod
    * LB + ASG - prod.
    * ASG only (non web apps that are not public)
* components
    * application
    * version
    * Environments
* Supports most common platforms - java, python etc. code needs to be uploaded

[back](index.md)
