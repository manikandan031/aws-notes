**Regions, Availibility Zones and IAM**

[back](index.md)

* AWS has a set of regions around the world. ex. us-east-1
* Each region has a cluster of data centers
* AWS services are region scoped
* Each region has 2 to 6 availability zones. Usually 3. ex. us-east-1a, us-east-1b
* Each AZ has 1 or more data centres with redundant power, networking and connectivity

**Choosing a Region**
* Compliance - Some governments do not allow data to leave the region
* Proximity to users
* Pricing

**IAM ( Identity and Access Management )**
* IAM. Is a global service. Not tied to a region.
* Has users, groups and roles
* The root account should not be used
* Groups has users
* Roles are for internal usage within AWS. Roles are assigned to machines.
* Policies are JSON documents that define what users / groups / roles can and cannot do.
* Least privilege principle - give each user the least amount of permissions to do their job.
* IAM Federation - Big enterprises can integrate their Active Directory / User repository with AWS IAM so that Users can SSO. Uses SAML Standard.

**IAM MFA Device Options**
* Virtual MFA device
    * Google Authenticator
    * Authy
* U2F (Universal 2nd factor) Security Key
    * Yubikey
* Hardware MFA device
    * Gemalto token

**Accessing AWS**
* AWS console - MFA
* AWS CLI - access keys
* AWS SDK - programmatic access - access keys

**Auditing**
* Credentials Report - Account level details of password resets, last used dates, mfa enabled etc.
* Access Advisor - User level details of whether a AWS service is being used or not. Can be used to revise the permissions.

**Budgets**
* Budgets can be used to set up alerts when the actual or forecasted cost exceeds threshold value.

[back](index.md)
