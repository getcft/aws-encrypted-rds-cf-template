# aws-encrypted-rds-cf-template

## Description:

This solution creates an encrypted [AWS RDS](https://aws.amazon.com/rds/) MySQL database leveraging a [AWS KMS](https://aws.amazon.com/kms/) key into a [VPC](https://aws.amazon.com/vpc/) private subnet zone.

The AWS CloudFormation template creates a AWS KMS encryption key for RDS, and an encrypted RDS MySQL instance leveraging the KMS key as well as a VPC with public and private subnets.

AWS RDS encrypted DB instances use the industry standard AES-256 encryption algorithm to encrypt your data on the server that hosts your Amazon RDS DB instances. Once your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance. You don't need to modify your database client applications to use encryption.

_***note AWS RDS, and KMS will incur costs**_

* [RDS MySQL pricing](https://aws.amazon.com/rds/mysql/pricing/) resource used in example: db.t2.small
* [KMS pricing](https://aws.amazon.com/kms/pricing/) resource used in example: 1 KMS key

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Use the Oregon region us-west-2 for the example
* IAM user with AWSKeyManagementServicePowerUser, AWSCloudFormationReadOnlyAccess, AmazonRDSFullAccess, AmazonVPCFullAccess

## See how it works:

AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation encrypted-rds-cf-template.yml (from the repo you cloned)

CloudFormation Fields

* Stack name (Enter a name to associate to your AWS VPC and RDS deployment) **Next**
* Continue choosing **Next**
* Check the box that says "I acknowledge that AWS CloudFormation might create IAM resources with custom names." and click **Create**

## Test:

In the AWS Management Console you should be able to verify the following have been created:

* 1 Public Subnet 10.0.10.0/24 (Zone A)
* 1 Private Subnet 10.0.20.0/24 (Zone A)
* 1 Public Subnet 10.0.30.0/24 (Zone B)
* 1 Private Subnet 10.0.40.0/24 (Zone B)
* 5 Route table entries to route either within 10.0.0.0/16 or to the either the Internet Gateway or NAT Gateway for outbound
* 1 Internet Gateway
* 1 RDS MySQL instance (db.t2.small) in a Private Subnet (user: dbuser pass: Passw0rd! )
* 1 RDS Security Group with port 3306 open to 10.0.0.0/16
* 1 RDS Subnet Group with 10.0.20.0/24 and 10.0.40.0/24
* 1 KMS Key (alias rds)

## Other Things:

* Obviously change the password
* For RDS password management you may want to look into [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
* The private subnets that form the RDS Subnet Group are private and have no gateway to the internet
* If you need your private subnets to have internet access for updates etc create a AWS NAT Gateway for outbound
