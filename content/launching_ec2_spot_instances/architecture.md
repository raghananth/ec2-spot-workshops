+++
title = "Architecture"
weight = 20
+++

In this workshop, you will deploy the following:

* AWS CloudFormation stack, which will include:
	* Amazon Virtual Private Cloud (Amazon VPC) with public subnets in two Availability Zones
	* AWS Cloud9 environment
	* Supporting IAM policies and roles
	* Supporting security groups
* Amazon EC2 launch template

You will be creating Spot instances using different AWS Services:

1. Amazon EC2 Auto Scaling group with On-Demand and Spot instances. The resulting architecture: ![Architecture using Amazon EC2 Auto Scaling](/images/launching_ec2_spot_instances/architecture_asg.jpg)

1. Amazon EC2 Fleet with On-Demand and Spot instances. The resulting architecture : ![Architecture using Amazon EC2 Auto Scaling](/images/launching_ec2_spot_instances/architecture_ec2_fleet.jpg)

1. Amazon Spot Fleet with Spot Instances. The resulting architecture : ![Architecture using Amazon EC2 Auto Scaling](/images/launching_ec2_spot_instances/architecture_spot_fleet.jpg)

1.  Amazon EC2 Spot Instance. The resulting architecture : ![Architecture using Amazon EC2 Auto Scaling](/images/launching_ec2_spot_instances/architecture_spot_instance.jpg)


