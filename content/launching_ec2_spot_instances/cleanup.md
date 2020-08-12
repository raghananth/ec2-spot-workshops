+++
title = "Clean Up"
weight = 150
+++

### Delete Your Auto Scaling Group

**To delete your Auto Scaling group using the console**

```bash
$ aws autoscaling delete-auto-scaling-group --auto-scaling-group-name SpotInstanceASG --force-delete
```

### Delete your EC2 Fleet

When you are finished using your EC2 Fleet, you can delete the EC2 Fleet
and terminate all of the running instances.

**To delete your EC2 Fleet and terminate the running instances**

```bash
$ aws ec2 delete-fleets --fleet-id fleet-e678bfc6-c2b5-4d9f-8700-03b2db30b183 --terminate-instances 
```

### Cancelling your Spot Fleet Request

When you are finished using your Spot Fleet, you can cancel the Spot Fleet request. This cancels all Spot requests associated with the Spot Fleet, so that no new Spot Instances are launched for your Spot Fleet.
You must specify whether the Spot Fleet should terminate its Spot Instances. If you terminate the instances, the Spot Fleet request enters the cancelled\_terminating state. Otherwise, the Spot Fleet request enters the cancelled\_running state and the instances continue to run until they are interrupted or you terminate them manually.

**To cancel and delete your EC2 Spot Fleet and terminate the running instances**

```bash
$ aws ec2 cancel-spot-fleet-requests --spot-fleet-request-ids sfr-b5988c3c-e5a3-4648-ac71-88eaf0f4c11e --terminate-instances 
```

### Terminating your Spot Instance

Terminating a Spot Instance request does not terminate the Spot instance. Terminate the Spot Instance Request and the Spot Instance.

**To terminate your Spot Instance Request**

```bash
$ aws ec2 cancel-spot-instance-requests --spot-instance-request-id sir-wxz8bjpq
```

**To terminate all your Spot Instance Requests using the console**

Go to [EC2 Instances] (https://console.aws.amazon.com/ec2/v2/home). 

Select the Spot Requests and select all the Spot requests.

Click on Actions, Cancel request. 

**To terminate your Spot Instance using the console**

Go to [EC2 Instances] (https://console.aws.amazon.com/ec2/v2/home?#Instances). 

Select the instance with Name as *EC2SpotImmersionDay* and status is *running*. 

Click on Actions, Instance State, then Terminate. 

### Deleting the Launch Template

If you no longer require the launch template, you can delete it. Deleting the launch template deletes all of its versions.

**To delete the launch template**

```bash
$ aws ec2 delete-launch-template --launch-template-name SpotInstanceTemplate
```

### Deleting the Cloud​Formation stack

Finally, delete the CloudFormation stack itself. This will delete the Cloud9 environment along with the initial VPC and subnets created.

**To delete the CloudFormation stack**

```bash
$ aws cloudformation delete-stack --stack-name $stack_name
```
