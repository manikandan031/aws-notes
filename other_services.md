**Other Services**

[back](index.md)

* CI/CD - AWS CodeCommit (like git), AWS CodeBuild (Build), AWS CodeDeploy(Deploy) and AWS CodePipeline (orchestrator, add manual approvals, stages etc)
* CloudFormation 
  * Infrastructure as code in AWS
  * uploaded in S3, to update a new version needs to be uploaded in S3
  * can create multiple stacks to separate concerns
  * every resource created via a CF gets a tag and easy to estimate costs of entire stack
  * templates can be edited via a CF designer
  * Template
    * Resources
    * Parameters
    * Mappings - static variables
    * Outputs - references to what has been created
    * Conditionals - conditions to check for resource creation
    * helpers - references and functions
  * Stack sets - can deploy same CF stack across different regions / aws accounts
* STEP functions
    * serverless workflow to orchestrate lambda functions
    * State machine
    * possibility for human approaval
    * use cases - workflows, order fulfillment etc 
* SWS Simple Workflow service
    * similar to Step functions but it runs on EC2 (not serverless)
* EMR Elastic MapReduce
    * Helps creating hadoop clusters with 100s of EC2 instances
    * supports Spark, HBase, Presto, Flink
    * auto scaling and integrated with EC2 instances
*OpsWorks
    * Chef and Puppet helps perform server configuration automatically. works well with EC2 and VMs.
    * OpsWorks is managed Chef and Puppet. Similar to AWS SSM.
    * Configuration as code
*ElasticTranscoder
    * convert media files into various formats. serverless.
*AWS Workspaces
    * managed cloud secure desktop. alternative to VDI.
* AppSync
    * Store and sync data across mobile and web apps realtime
    * uses GraphQL
* Cost Explorer
    * visualize and manager aws costs and usage data
    * provides recommendataions on savings plans

    
[back](index.md)