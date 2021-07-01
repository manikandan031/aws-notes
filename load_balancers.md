**Load Balancers**
* **Types**
    * Class Load Balancer (Legacy)
    * Application Load Balancer (Layer 7)
    * Network Load Balancer (Layer 4)
    * Gateway Load Balancer
* **Use cases**
    * Spread traffic 
    * Horizontal scaling
    * Expose a single DNS
    * Regular Health checks of apps
    * SSL termination
    * Session stickiness
    * High availability across zones
    * Separate Public and private traffic
* **Application Load Balancer**
    * Single Load Balancer can route traffic to different target groups based on routing rules
    * Routing rules can be based on path / query params
    * Access logs available for every request
    * Routing rules can be configured to return different response codes based on url
    * Supports Http, Https and web socket
    * Cross Zone load balancing is enabled by default. No charges.
* **Network Load Balancer**
    * TCP, TLS and UDP
    * Does not terminate connection from client
    * Used for extreme performance use cases like load balancing tcp traffic for a Database.
    * Cross Zone load balancing is disabled by default. If enabled additional charges.
* **Load Balancer Security Groups**
    * Your Target groups will be in a security group
    * Your Load balancer will be in a security group
    * The Target security group should allow inbound traffic from the load balancer security group.
* **SNI (Server Name Indication)**
    * Load balancers can perform SSL termination. Should configure certificates along with rules. Certificates can be managed in ACM.
    * SNI allows the ability to manage multiple ssl certificates and route to multiple web sites from a single web server.
    * For SNI, the clients should mention the hostname to which they want to communicate with.
    * Based on the hostname, the LB will attach the corresponding SSL certificate.
* **Connection Drainig / Deregistration delay**
    * When a EC2 instance is shutting down it will enter draining mode
    * ELB will route all new traffic to other ec2 instances
    * Existing connections will get 5 mins to complete.
* Target Groups can be instances, IP addresses and lambda functions
* **Auto Scaling Groups**
    * Scale in and Scale out EC2 instances and automatically attach them to load balancers
    * Provide a launch template while defining the ASG
    * Scaling policy can be set up based on 
        * Cpu, memory usage
        * cloud watch alarms. Cloud watch alarms can be based on default or custom metrics.
        * Schedule
    * Can connect ASG with Health check done by load balancer to terminate unhealthy instances.
    * ASG has a default cool down period of 300 seconds to ensure scaling doesn’t start before the previous scaling takes effect.
    * ASG default termination policy
        * Finds the AZ that has the highest number of instances
        * Finds the instance with the oldest launch configuration and terminates it.
    * Provides life cycle hooks in pending state and before termination state
