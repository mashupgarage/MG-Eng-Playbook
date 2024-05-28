# Amazon EC2 (Elastic Compute Cloud)

## Basics
Your basic on-demand, scalable computing service hosted by AWS
One can launch many instances as needed
Easy to scale depending on the demand:
  * processing aggregated reports
  * seasonal user base (user volume on Christmas season)

Available in different OS flavors:
  * Windows
  * Linux
  * OSX

## Availability Zones (AZ)
Your data centers where your EC2 instances are localted
Said to be fault tolerant and highly available
They are under **regions**:
  * ap-southeast-1 (Asia pacific Singapore)

**Multi-AZ** redundancy feature:
* Whenever an AZ fails, there is a failover mechanism that takes over
* It is another AZ but withing the same region

## Virtual Private Cloud (VPC)
Defines a virtual private network for your AWS resource (EC2, RDS etc.)
Able to configure:
* IP address ranges
* Subnets
* Configure routing tables (simply where packets will be redirected)
* VPC's by default, is configured with a route to an internet gateway (in short, EC2 instances comes with internet by default)
* By default, public IP addresses and DNS hostnames are assigned as well

## Security Groups
Are a set of rules where one can specify protocal, port ranges etc.
Classified into 2 types:
* Inbound
  * set of rules for inbound traffic
* Outbound
  * set of rules for outbound traffic
