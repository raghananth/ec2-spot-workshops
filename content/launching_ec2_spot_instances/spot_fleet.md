+++
title = "Launching EC2 Spot Instances via Spot Fleet"
weight = 120
+++

You can create a Spot Fleet request and specify a launch template in the instance configuration. When Amazon EC2 fulfills the Spot Fleet request, it uses the launch parameters defined in the associated launch template.

**To create a new EC2 Fleet using the command line, run the following**

1. Open [**config.json**] (https://raw.githubusercontent.com/raghananth/ec2-spot-workshops/update-launch-ec2-spot-instance-workshop/workshops/launching_ec2_spot_instances/config.json) **NOTE: CHANGE THIS LINK TO MASTER WHEN MERGING** on the Cloud9 editor and review the configuration. Pay special attention at the Overrides and the InstancesDistribution configuration blocks and try to guess how many instances of which instance types will be launched. 

2. You will notice there are placeholder values for %publicSubnet1%, %publicSubnet2%, %launchTemplateId% and %accountId%. To update the configuration file with the outputs from the CloudFormation template, execute the following command:

    ```bash
    $ sed -i.bak -e "s#%publicSubnet1%#$publicSubnet1#g" -e "s#%publicSubnet2%#$publicSubnet2#g" -e "s#%spotFleetRole%#$spotFleetRole#g" -e "s#%launchTemplateId%#$launchTemplateId#g" config.json
    ```

3. Save the file and create the spot fleet:

    ```bash
    $ aws ec2 request-spot-fleet --spot-fleet-request-config file://config.json
    ```

    **Example return**

    ```bash
    {
        "SpotFleetRequestId": "sfr-b5988c3c-e5a3-4648-ac71-88eaf0f4c11e"
    }
    ```

## Monitoring Your Spot Fleet

The Spot Fleet launches Spot Instances when your maximum price exceeds
the Spot price and capacity is available. The Spot Instances run until
they are interrupted or you terminate them.

To view the spot fleet details:

```bash
$ aws ec2 describe-spot-fleet-requests --spot-fleet-request-ids sfr-b5988c3c-e5a3-4648-ac71-88eaf0f4c11e
```
