---
title: "Launching EC2 Spot Instances"
date: 2019-01-26T00:00:00Z
weight: 25
pre: "<b>⁃ </b>"
---


## Overview

**Amazon EC2 Spot** instances is Spare Amazon EC2 compute capacity that is available at savings of up to 90% off On-Demand prices. Amazon EC2 Spot instances are ideal for various stateless, fault-tolerant, or flexible applications including web server, CI/CD, and test & development workloads. EC2 Spot enables you to

* run EC2 instances at low, predictable prices to optimize compute cost over On-Demand and Reserved instances
* scale the EC2 instances based on workload needs without significant increase in budget

Amazon EC2 Spot instances can be provisioned by a number of Services and APIs. This lab will walk through 4 different ways :

* Amazon EC2 Auto Scaling group
* Amazon EC2 Fleet API
* Spot Fleet API
* RunInstances API

This lab utilizes Launch Templates to streamline and simplify the launch process. Launch template help reduce the number of steps to create instances by capturing all launch parameters within one resource. Hence making it easier to implement standards and best practices, improve security posture and minimize the risk of deployment errors.

The lab will conclude with a Best Practices for launching Amazon EC2 Spot instances.

## Pre-Requisites for this lab:

 - A laptop with Wi-Fi running Microsoft Windows, Mac OS X, or Linux.
 - The AWS CLI installed and configured.
 - An Internet browser such as Chrome, Firefox, Safari, or Edge.
 - An AWS account. You will create AWS resources including IAM roles during the workshop.
