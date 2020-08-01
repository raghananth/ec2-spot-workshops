+++
title = "Launching EC2 Spot instances via EC2 Auto Scaling Group"
weight = 100
+++

## Launching EC2 Spot Instances via an EC2 Auto Scaling Group

Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.  You create collections of EC2 instances, called Auto Scaling groups.  You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size.

With launch templates, you can also provision capacity across multiple instance types using both On-Demand Instances and Spot Instances to achieve the desired scale, performance, and cost.

1. Open [**asg.json**](https://raw.githubusercontent.com/raghananth/ec2-spot-workshops/update-launch-ec2-spot-instance-workshop/workshops/launching_ec2_spot_instances/asg.json) **NOTE: CHANGE THIS LINK TO MASTER WHEN MERGING** on the Cloud9 editor and review the configuration. Pay special attention at the **Overrides** and the **InstancesDistribution** configuration blocks and try to guess how many instances of which instance type and which purchase option will be launched. Take a look at our [docs](https://docs.aws.amazon.com/autoscaling/ec2/userguide/asg-purchase-options.html#asg-allocation-strategies) to review how InstancesDistribution and allocation strategies work.
<div>
  {{% expand "Help me understand the AutoScaling configuration" %}}

  The **Overrides** configuration block provides EC2 AutoScaling the list of instance types your workload can run on. As Spot instances are **spare** EC2 capacity, your workloads should be flexible to run on multiple instance types and multiple availability zones; hence leveraging multiple *spot capacity pools* and making the most out of the available spare capacity. To select a list of instance types for your workload you can use [Spot Instance Advisor](https://aws.amazon.com/ec2/spot/instance-advisor/) which will help you filtering suitable instances by number of vCPUs and amount of memory and also provide you data about the interruption rate during the last 30 days for each instance type, so you can pick a list of best-suited instance types with low interruption rates.

  Then, the *InstancesDistribution* configuration block determines how EC2 AutoScaling picks the instance types to use, while at the same time it keeps a balanced number of EC2 instances per Availability Zone.

  * The **prioritized** allocation strategy for on-demand instances makes AutoScaling try to launch the first instance type of your list and skip to the next instance type if for any reason it's unable to launch it (e.g. temporary unavailability of capacity). This is particularly useful if you have Reserved Instances for your baseline capacity, so AutoScaling launches the instance type matching your reservations.
  * **OnDemandBaseCapacity** is set to 2, meaning the first two EC2 instances launched by EC2 AutoScaling will be on-demand.
  * **OnDemandPercentageAboveBaseCapacity** is set to 0 so all the additional instances will be launched as Spot Instances
  * **SpotAllocationStrategy** is lowest-price, which instructs AutoScaling to pick the cheapest instance type on each Availability Zone.
  * **SpotInstancePools** is 4, which tells AutoScaling to launch instances across the 4 cheapest instance types on each Availability Zone for the list of instances provided on the overrides; diversifying our fleet acquiring capacity from multiple *Spot pools* and reducing the likelihood of a large portion of our fleet to be interrupted in a short period of time. 

  {{% /expand %}}
</div>

2. You will notice there are placeholder values for **%publicSubnet1%** and **%publicSubnet2%**. To update the configuration file with the outputs from the CloudFormation template, execute the following command:

    ```bash
    $ sed -i.bak -e "s#%publicSubnet1%#$publicSubnet1#g" -e "s#%publicSubnet2%#$publicSubnet2#g" asg.json
    ```

3. Save the file and create the auto scaling group:

    ```bash
    $ aws autoscaling create-auto-scaling-group --cli-input-json file://asg.json
    ```
{{% notice note %}}
This command will not return any output if it is successful.
{{% /notice %}}

4. Browse to the [Auto Scaling console](https://console.aws.amazon.com/ec2/autoscaling/home#AutoScalingGroups:view=details) and check out your newly created auto scaling group. Take a look at the instances it has deployed.


## Optional exercise

Now that you have deployed an EC2 AutoScaling group with Mixed Instance Types and Purchase Options, take some time to manually scale out and scale in the number of instances of the group and see which instance types AutoScaling launches. Also, modify the SpotInstancePools parameter and experiment with the [capacity-optimized](https://aws.amazon.com/blogs/compute/introducing-the-capacity-optimized-allocation-strategy-for-amazon-ec2-spot-instances/) allocation strategy to get a good grasp of how the different allocation strategies behave. 