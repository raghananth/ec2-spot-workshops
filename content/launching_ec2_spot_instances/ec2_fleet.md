+++
title = "Launching EC2 Spot Instances via an EC2 Fleet"
weight = 110
+++

## Launching EC2 Spot Instances with On-Demand Instances via an EC2 Fleet

An *EC2 Fleet* contains the configuration information to launch a
fleet—or group—of instances. In a single API call, a fleet can launch
multiple instance types across multiple Availability Zones, using the
On-Demand Instance, Reserved Instance, and Spot Instance purchasing
models together. Using EC2 Fleet, you can define separate On-Demand and
Spot capacity targets, specify the instance types that work best for
your applications, and specify how Amazon EC2 should distribute your
fleet capacity within each purchasing model.

**To create a new EC2 Fleet using the command line, run the following**

```bash
$ aws ec2 create-fleet --launch-template-configs LaunchTemplateSpecification="{LaunchTemplateName=SpotInstanceTemplate,Version=1},Overrides=[{SubnetId=$publicSubnet1},{SubnetId=$publicSubnet2}]" --target-capacity-specification TotalTargetCapacity=4,OnDemandTargetCapacity=1,DefaultTargetCapacityType=spot
```

**Example return**

```bash
{
"FleetId": "fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183"
}
```

This EC2 Fleet has requested a total capacity of 4 instances- 1 On-Demand and 3 Spot.

**Check them out by running**

```bash
$ aws ec2 describe-fleets --fleet-ids fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183
```

and

```
$ aws ec2 describe-fleet-instances --fleet-id fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183
```

