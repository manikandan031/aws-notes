**IAM Advanced**

[back](index.md)

**AWS STS**
* Used to provide temporary access to aws resources
* token is valid for 1 hr and then needs to be refreshed
* AssumeRole - within or cross account access for aws users
    * Create a role with necessary permissions (may be another account)
    * User calls AssumeRole api to reach STS for a temporary credentials
    * STS checks with IAM to check if the user has the permissions. If yes, STS returns temporary credentials.
* AssumeRoleWithSAML - for federated users with SAML
* AssumeRoleWithWebIdentity - used for facebook / google / OIDC login. not recommended. aws recommends to use cognito instead.
* GetSessionToken - for MFA
* Identity Federation - for non aws users. User management is outside AWS
    * SAML 2.0 - for internal / org. users 
        * user logs into identity provider with saml
        * user sends saml assertion to sts requesting access using AssumeRoleWithSAML
        * sts validates saml token with idp and sends aws temporary credentials
        * this is old way. new say is to use AWS SSO.
    * Custom Identity Broker
      * necessary only if ur idp is not SAML 2.0 compatible
      * Custom layer to be written 
    * Web Identity Federation with / without cognito - for anonymous users 
        * cognito is recommended
        * direct access from client (mobile / browser) to aws resources without creating millions of users on iam
        * user logs into facebook / google. sends the token to cognito federated identity. cognito verifies the token with the provider. then gets temp. credentials from STS and returns.
    * Non SAML with Microsoft AD
      * AWS Managed AD + On Prem AD 
      * AD connector to proxy from aws to on prem AD
      * AWS simple AD if we dont have any on prem AD
    

**AWS organizations**

* Managing multiple aws accounts in organization
* ability to manage multiple aws accounts
* can get global billing
* there is a main account and a group of member accounts
* member accounts can be for a department / cost center or resource isolation
* this is different from 1 account with multi - VPC
* OU
    * we can have multiple OUs within the master account
    * member accounts within each OUs
    * SCPs (Service Control Policies) can be set at OU level to deny access to say some specific services.
    * SCPs cant be applied to master accounts.
    
**IAM Advanced**

* IAM conditions
    * notIPAddress - aws::sourceIP
    * resourceRegion
    * resourceTags
    * enforce MFA
* resourcePolicy vs AssumeRole - resourcePolicy allows to retain original role and its permissions whereas assumeRole will lose original role permissions.
* IAM for S3 - Resource: ["arn:aws:s3:::test/*"] - /* for policy on objects inside bucket.
* IAM permission boundaries - can be set on top of iam permissions.
* IAM permissions is intersection of - SCPs & identity based Policy & IAM Permission boundaries.

**Resource Access Manager**

* used to share resources like VPCs and subnets across aws accounts.
* If we want our aws resources to be managed from different aws accounts but they need to in the same subnet.

**AWS SSO**

* it is like a IDP within AWS
* useful for accessing multiple accounts and business applications with a single sign in
* can talk to on prem AD or aws managed AD to get the users.
* has integration with OUs and business applications like office 365, slack etc..
* provides its own login portal


[back](index.md)

    
