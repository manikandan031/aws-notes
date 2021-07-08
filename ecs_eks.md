**ECS**

[back](index.md)

* Elastic container service is used to deploy docker containers in AWS.
* Launch Types - _EC2 & Fargate_
    * **EC2** 
        * an ASG of EC2 instances is created. The ASG is across AZs.
        * an ECS agent runs on each EC2 instance. This registers the EC2 instance in the ECS cluster.
        * ECS tasks are run on ec2 instances
    * **Fargate**
        * Serverless offering
        * ECS tasks are created and run on Fargate cluster without EC2 instances.
        * Each task has a ENI and hence a unique IP.
* **Iam Roles**
    * EC2 Instance Profile - used by ecs agent. The agent needs permissions to talk to ECS service, send logs to cloud watch, pull images from ECR etc.
    * ECS Task Role - use IAM roles for ECS tasks for the permission it needs.
    * EC2 Launch Type Load balancing - must allow access to all ports on the ECS instance SG from the ALB SG.
    * Fargate Launch Type Load balancing - must allow access to the ECS task port on the ALB SG.
* Scheduled running of ECS tasks
    * **Amazon Event bridge** can be used to launch ECS tasks based on a event notification from S3.
* Autoscaling - Simple to add or remove ECS tasks based on avg. cpu / memory / sqs queue length etc.
* **Rolling Updates**
    * Minimum Healthy Percent - 100 , Maximim Percent - 200 - Based on these 2 parameters old tasks will be terminated and new tasks will be launched.
* **ECR** Elastic Container Registry - private docker image registry in AWS
* **EKS** Elastic Kubernetes Service - AWS managed Kubernetes Service    

[back](index.md)


    

         
