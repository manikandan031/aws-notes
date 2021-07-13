**Security**

[back](index.md)

**Key Management Service (KMS)**
* Used to create and manage encryption keys for symmetric and asymmetric encryption.
* also contains pre-existing aws managed keys that are used internally by aws.
* internally integrated with systems manager / Parameter store and secrets manager to encrypt secrets.
* integrated with EBS to encrypt volumes, s3 to encrypt objects, rds & redshift to encrypt data and lots more. 
* Users cannot access the symmetric keys or the private asymmetric keys. need to call the kms api to encrypt or decrypt.
* user managed keys costs 1$ per month.
* can audit the kms apis in cloudtrail
* can encrypt only upto 4KB. for more than 4kb use envelope encryption.
* kms keys are bound to specific region. access to kms keys is controlled by kms key polocies.
* auto key rotation can be configured for customer managed keys for every 1 year.
* manual key rotation can be done if needed. In this case the key id will change. so better to use aliases in code.

**SSM Parameter store / System Manager**
* secure storage for configuration and secrets.
* seamless integration with kms to encrypt secrets like passwords.
* version tracking is available out of the box.
* Stores in a hierarchical manner ex. my-app/dev/db-url, my-app/dev/db-password.
* you can get parameters by name or by path.
* standard tier free 10000 parameters, advanced tier upto 100000 parameters.

**Secrets Manager**
* newer service compared to systems manager. serves similar purpose.
* has capability to force rotation of secrets automatically using lambda integration.
* has deeper integration with rds

**CloudHSM**
* aws only provides the ecryption hardware. hardware is tamper resistent.
* client have to use their own software to manager encryption keys.
* aws will not have access to your keys and cannot recover them.

**AWS Shield**
* protects from DDos attacks
* free tier provides some basic protection from layer 7 / laer 4 attacks.
* Shield advanced - more sophisticated protection with a 24/7 DRP team. waiver from any higher costs due to ddos. 3000$ per month.

**WAF Web application firewall**
* Layer protection against attacks like sql injection, cross site scripting etc.
* WAF can be deployed with ALBs / Api Gateway / CloudFront Distribution.
* Web ACL rules are defined to restrict IPs / Http Headers / Size constraints / Geo match / rate based rules per IP etc.
* AWS Firewall manager used to manage rules for all accounts across ur organization.

**Guard Duty**
* uses ML algorithms, anamoly detection to detect attacks in your account.
* input - cloud trail logs, VPC flow logs, DNS logs.
* can set CW event rules with SNS integration to get email alerts.
* can protect against crypto currency attacks.

**Inspector**
* to perform automated security assessment on ec2 instances.
* runs as an agent in EC2 instances.
* generates a report and there is integration with SNS.

**Macie**
* to perform data security scanning for PII (Personal identifiable information)
* can scan S3 buckets and notify via CW events.

[back](index.md)


