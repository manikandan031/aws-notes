**Cloud Front**

[back](index.md)

* CloudFront is AWS CDN network used to speed up reads
* Has 216 edge locations across globe
* Used to cache content at edge locations to speed up access to content from S3 or any Http based origins
* Also provides protection from DDos with AWS Shield and AWS Web application Firewall
* Origins - S3 content, Static S3 website, EC2, Load balancers
* OAI Origin Access Identity - used to ensure S3 content can ONLY be accessed via cloudfronts
* Security Groups - ALBs or EC2 should allow incoming traffic from all IP addresses of edge locations.
* Geo Restriction - can be used to allow access to resources only from specific geographic location. Uses 3rd party geo ip db. Useful for Copyright laws
* Cloud front is global vs S3 cross region replication is useful for 1or 2 regions.
* Cloud front provides signed URLs and signed cookies which can be used to give time based temporary access to content.
* Pricing
    * Price class All
    * Price class 200
    * Price class 100
* Routing rules can be added in edge locations to route based on content-type or path patterns
* CF Origin Groups - to have multiple origins primary and secondary and use it for failover.
* Field Level encryption - can be used to encrypt individual fields
* Useful for caching and serving media content like images / videos

**Global Accelerator**
* Uses Anycast Ips - multiple servers have the same IP. Request goes to the nearest server.
* Used to reduce number of hops to reach server. Makes use of edge locations and AWS private network to minimise latency
* As compared to CF there is no caching here. All requests goes to the servers, but it goes from edge locations to origins via private network.
* Health checks and fail over
* Useful for non http use cases like IOT, gaming etc.

[back](index.md)
