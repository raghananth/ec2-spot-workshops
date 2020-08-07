+++
title = "Launching an EC2 Spot Instance via the RunInstances API"
weight = 130
+++

    * Placement option for an instance like Dedicated host or AZ or placement group
    * Instance Shutdown Behavior - instance stops or terminates when you initiate shutdown from the instance
    * Option to launch instances with instance metadata access Turn on or Off.
    * Option to protect instance termination from EC2 Console
    * Support for Spot Blocks


## Launching an EC2 Spot Instance via the RunInstances API

If there is a need to create EC2 instances in a dedicated host or Availability Zone or placement group, Run Instances API can be used to provision EC2 Spot instances. 

Run Instance API supports Instance Shutdown behaviour - terminate, stop, and hibnernate. This is useful if you are targetting capacity reservation.

**To create a new EC2 Spot Instance using the command line, run the following**

To launch an EC2 Spot Instance from a launch template using the command
line, use the run-instances AWS CLI command and specify the
*--launch-template* parameter as well as the *--instance-market-options*
parameter.

    ```bash
    $ aws ec2 run-instances --launch-template LaunchTemplateName=SpotInstanceTemplate,Version=1 --instance-market-options MarketType=spot --subnet-id $publicSubnet1
    ```

That is all there is to it\! You can see your Spot Instance request in
the Spot console at <https://console.aws.amazon.com/ec2spot>.

![RunInstances API](/images/launching_ec2_spot_instances/runinstances_api_image_1.png)
