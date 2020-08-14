+++
title = "Launching EC2 Spot Instances using EC2 Fleet"
weight = 110
+++

[**EC2 Fleet**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet.html) contains the configuration information to launch a fleet—or group—of instances. In a single API call, a fleet can launch multiple instance types across multiple Availability Zones, using the On-Demand Instance, Reserved Instance, and Spot Instance purchasing models together. Using EC2 Fleet, you can define separate On-Demand and Spot capacity targets, specify the instance types that work best for your applications, and specify how Amazon EC2 should distribute your fleet capacity within each purchasing model.

EC2 Fleet could be used to provision EC2 Spot instances if multiple configuration options (i.e different EBS volume sizes for different instance types) and multiple launch templates are needed to create the EC2 instances. Unlike EC2 Auto Scaling, EC2 Fleet does not ensure that instances are spread across all AZs. In most cases, EC2 Auto Scaling is the preferred over EC2 Fleet.

EC2 Fleet can be used to simplify the provision of capacity using any combination of purchase options - On Demand, Reserved and Spot. EC2 Fleet lets you scale to a large number of vCPU or instance needs and can customize the fleet based on application needs - based on number of cores or instances, or amount of memory. You can assign weightages to the different instances that is meaningful to your application scaling.

EC2 Fleet provides three types of allocation strategies that can be used for Spot Instances:

* **capacity-optimized** allocates Spot Instances from the pool with optimal capacity for the number of instances that are launching.
* **diversified** allocates Spot Instances that are distributed across all pools.
* **lowest-price** allocates Spot Instances from the pool with the lowest price. This is the default strategy.

For more information on Spot allocation strategies, check out [EC2 Fleet - Spot allocation strategies](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-configuration-strategies.html#ec2-fleet-allocation-strategy)

**To create a new EC2 Fleet using the command line, run the following**

```bash
$ aws ec2 create-fleet --launch-template-configs LaunchTemplateSpecification="{LaunchTemplateName=SpotInstanceTemplate,Version=1},Overrides=[{SubnetId=$publicSubnet1},{SubnetId=$publicSubnet2}]" --target-capacity-specification TotalTargetCapacity=4,OnDemandTargetCapacity=1,DefaultTargetCapacityType=spot --spot-options AllocationStrategy=capacity-optimized
```

**Example return**

```bash
{
    "FleetId": "fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183"
}
```

This EC2 Fleet has requested a total capacity of 4 instances- 1 On-Demand and 3 Spot.

#### View the details of the EC2 Fleet

**To view the EC2 fleet details using the command line, run the following**

```bash
$ aws ec2 describe-fleets --fleet-ids fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183
```

and

```bash
$ aws ec2 describe-fleet-instances --fleet-id fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183
```

