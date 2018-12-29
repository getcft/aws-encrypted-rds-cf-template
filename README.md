# aws-encrypted-rds-cf-template

## Description:

This solution creates an encrypted [AWS RDS](https://aws.amazon.com/rds/) MySQL database leveraging a [AWS KMS](https://aws.amazon.com/kms/) key into a [VPC](https://aws.amazon.com/vpc/) private subnet zone.

The AWS CloudFormation template creates a AWS KMS encryption key for RDS, and an encrypted RDS MySQL instance leveraging the KMS key as well as a VPC with public and private subnets and an EC2 Bastion host for access to the RDS instance.

AWS RDS encrypted DB instances use the industry standard AES-256 encryption algorithm to encrypt your data on the server that hosts your Amazon RDS DB instances. Once your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance. You don't need to modify your database client applications to use encryption.

_***note AWS RDS, KMS, and EC2 will incur costs**_

* [RDS MySQL pricing](https://aws.amazon.com/rds/mysql/pricing/) resource used in example: db.t2.small
* [KMS pricing](https://aws.amazon.com/kms/pricing/) resource used in example: 1 KMS key
* [EC2 pricing](https://aws.amazon.com/ec2/pricing/on-demand/) resource used in example: t2.nano

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* Use the Oregon region us-west-2 for the example
* IAM user with AWSKeyManagementServicePowerUser, AWSCloudFormationReadOnlyAccess, AmazonS3FullAccess, AmazonRDSFullAccess, AmazonVPCFullAccess, AmazonEC2FullAccess

## See how it works:

AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation encrypted-rds-cf-template.yml (from the repo you cloned)

CloudFormation Fields

* Stack name (Enter a name to associate to your AWS VPC and RDS deployment) and choose an SshKeyName
you must have one created in your region then **Next**
* Continue choosing **Next**
* Check the box that says "I acknowledge that AWS CloudFormation might create IAM resources with custom names." and click **Create**

## Test:

* SSH with your EC2 keypair you selected when executing the CloudFormation template into the EC2 bastion host
* sudo yum install mysql
* At the command prompt: mysql -u dbuser -p -h (put your RDS endpoint here available in the AWS RDS console)
* When prompted for password use: Passw0rd!
* You should now be connected to your RDS MySQL instance

## Other Things:

* Obviously change the password
* For RDS password management you may want to look into [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
* The private subnets that form the RDS Subnet Group are private and have no gateway to the internet
* If you need your private subnets to have internet access for updates etc create a AWS NAT Gateway for outbound
