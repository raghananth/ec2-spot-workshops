+++
title = "Clone the GitHub repo"
weight = 60
+++

In order to execute the steps in the workshop, you'll need to clone the workshop GitHub repo.


1. In the Cloud9 IDE terminal, run the following command: **NOTE: CHANGE THIS LINK TO MASTER WHEN MERGING**

	```bash
	$ git clone https://github.com/raghananth/ec2-spot-workshops.git
	```
	
1. Change to branch: **NOTE: REMOVE THIS STEP WHEN MERGING**

	```bash
	$ cd ec2-spot-workshops
	$ git checkout update-launch-ec2-spot-instance-workshop
	```
	
1. Change into the workshop directory: **NOTE: CHANGE THIS LINK TO MASTER WHEN MERGING**

	```bash
	$ cd workshops/launching_ec2_spot_instances
	```

1. Feel free to browse around. You can also browse the directory structure in the **Environment** tab on the left, and even edit files directly there by double clicking on them.

2. During the workshop, you will need to modify the configuration files to refer to the identifiers of the resources created by the CloudFormation stack you deployed. To reduce copy and paste across the CloudFormation console and the Cloud9 environment, we will load the CloudFormation Stack **Outputs** to environment variables. During the workshop the instructions will provide [sed](https://linux.die.net/man/1/sed) commands to populate configuration files. Make sure you open them on the Cloud9 editor to review the files and understand the settings of the resources you will be launching.
	
	First, configure the stack_name environment variable with the name of your CloudFormation template. For example, if the name of your stack is **LaunchEC2Spot** run the following command:

	```bash
	$ export stack_name=LaunchEC2Spot
	```

	Now, load the CloudFormation stack outputs on environment variables running the following command:
	```bash
	$ export AWS_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)
	

	# load outputs to env vars
	$ for output in $(aws cloudformation describe-stacks --stack-name $stack_name --query 'Stacks[].Outputs[].OutputKey' --output text)
	do
    	export $output=$(aws cloudformation describe-stacks --stack-name $stack_name --query 'Stacks[].Outputs[?OutputKey==`'$output'`].OutputValue' --output text)
    	eval "echo $output : \"\$$output\""
	done

	```

	If successful, the output should be similar to the following:

	```bash
	spotFleetRole : arn:aws:iam::736405094009:role/LaunchEC2Spot-spotFleetRole-39D59A0GFPRW
    awsRegionId : us-west-2
    vpc : vpc-025a40d31afe98d12
    publicSubnet2 : subnet-0e6e5cc206fc084c6
    publicSubnet1 : subnet-0a055243ab4c080e8
    loadBalancerSecurityGroup : sg-0eb2a85966840efd8
    cloud9Environment : RunningEC2Spot
	```

	Lastly, store the account id into **accountId** variable

	```bash
	$ export accountId=$(aws sts get-caller-identity | jq -r .Account)
	```
