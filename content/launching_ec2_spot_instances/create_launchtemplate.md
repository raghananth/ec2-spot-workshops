+++
title = "Create Launch Template"
weight = 70
+++

## Creating a Launch Template 

You can create a *launch template* that contains the configuration
information to launch an instance. Launch templates enable you to store
launch parameters so that you do not have to specify them every time you
launch an instance. For example, a launch template can contain the AMI
ID, instance type, and network settings that you typically use to launch
instances. When you launch an instance using the Amazon EC2 console, an
AWS SDK, or a command line tool, you can specify the launch template to
use.

**To create a new launch template using the command line**

1. You'll need to gather the following data
    1. **AMI ID**: Specify an AMI ID from which to launch the instance.
        You can use an AMI that you own, or you can [find a suitable
        AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html).
    2. **Instance type**: Choose the instance type. Ensure that the
        instance type is compatible with the AMI you've specified. For
        more information, see [Instance
        Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html).
    3. **Subnet**: Specify the subnet in which to create a new network
        interface. For the primary network interface (eth0), this is the
        subnet in which the instance is launched.

2. The variable %ami-id% should contain the latest Amazon Linux 2 AMI, and instanceProfile and instanceSecurityGroup need to be populated with the resources created by your CloudFormation stack; which are available as Stack Outputs. We can pull the latest Amazon Linux 2 AMI with the AWS CLI, and as we have loaded our CloudFormation stack outputs as environment variables on a previous step, for convenience we can use the following commands to update your configuration file:

```bash
export ami_id=$(aws ec2 describe-images --owners amazon --filters 'Name=name,Values=amzn2-ami-hvm-2.0.????????-x86_64-gp2' 'Name=state,Values=available' --output json | jq -r '.Images |   sort_by(.CreationDate) | last(.[]).ImageId')
```
    
3. Once you've gathered the data, create the launch template from the command line as follows (be sure to change the following values: **SubnetId**, **ImageId**, **InstanceType**, **Tags** - **Value**):


```
aws ec2 create-launch-template --region $awsRegionId --launch-template-name SpotInstanceTemplate --version-description TemplateForSpotVersion1 --launch-template-data "{\"ImageId\":\"$ami_id\",\"InstanceType\":\"m4.large\",\"TagSpecifications\":[{\"ResourceType\":\"instance\",\"Tags\":[{\"Key\":\"Name\",\"Value\":\"EC2SpotImmersionDay\"}]}]}"
```

**Example return**

```bash
{
    "LaunchTemplate": {
        "LaunchTemplateId": "lt-0e550c0e16efb3829",
        "LaunchTemplateName": "SpotInstanceTemplate",
        "CreateTime": "2020-07-24T21:52:32.000Z",
        "CreatedBy": "arn:aws:iam::123456789012:user/xxxxxxxx",
        "DefaultVersionNumber": 1,
        "LatestVersionNumber": 1
    }
}
```

{{% notice info %}}
Note the **LaunchTemplateId** (eg. "lt-0e550c0e16efb3829") or
**LaunchTemplateName** (eg. "SpotInstanceTemplate") of the newly created 
Launch Template for the next steps.
{{% /notice %}}

