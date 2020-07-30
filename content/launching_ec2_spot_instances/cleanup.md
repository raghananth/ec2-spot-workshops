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
<!--
**To delete all EC2 Fleet and terminate the running instances**

```bash
$ for fleet_id in $(aws ec2 describe-fleets | jq -r ".Fleets[].FleetId") ; do aws ec2 delete-fleets --fleet-id $fleet_id --terminate-instances; done 
```
-->

### Cancelling your Spot Fleet Request

When you are finished using your Spot Fleet, you can cancel the Spot
Fleet request. This cancels all Spot requests associated with the Spot
Fleet, so that no new Spot Instances are launched for your Spot Fleet.
You must specify whether the Spot Fleet should terminate its Spot
Instances. If you terminate the instances, the Spot Fleet request enters
the cancelled\_terminating state. Otherwise, the Spot Fleet request
enters the cancelled\_running state and the instances continue to run
until they are interrupted or you terminate them manually.

**To cancel and delete your EC2 Spot Fleet and terminate the running instances**

```bash
$ aws ec2 cancel-spot-fleet-requests --spot-fleet-request-ids sfr-b5988c3c-e5a3-4648-ac71-88eaf0f4c11e --terminate-instances 
```

### Terminating a Spot Instance

**To terminate a Spot Instance using the console**

```bash
$ aws ec2 cancel-spot-instance-requests --spot-instance-request-id sir-wxz8bjpq
```

### Deleting a Launch Template

If you no longer require a launch template, you can delete it. Deleting
a launch template deletes all of its versions.

**To delete a launch template**

```bash
$ aws ec2 delete-launch-template --launch-template-name SpotInstanceTemplate
```
