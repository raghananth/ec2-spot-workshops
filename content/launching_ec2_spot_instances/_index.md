---
title: "Launching EC2 Spot Instances"
date: 2020-08-14T00:00:00Z
weight: 25
pre: "<b>⁃ </b>"
---

## Overview

Amazon EC2 Spot instances is Spare Amazon EC2 compute capacity that is available at savings of up to 90% off On-Demand prices. EC2
Spot enables you to

* run EC2 instances at low, predictable prices to optimize compute cost over On-Demand and Reserved instances
* scale the EC2 instances based on workload needs without significant increase in budget

This lab will walk you through different ways of running Amazon EC2 Spot instances :
* Amazon EC2 Auto Scaling group
* Amazon EC2 Fleet API
* Spot Fleet
* RunInstances API

The lab will create a EC2 Launch template which will be utilized in all the above steps. We will end this lab with a discussion on which is the most prefered method of provisioning Amazon EC2 Spot instances.

## Pre-Requisites for this lab:

 - A laptop with Wi-Fi running Microsoft Windows, Mac OS X, or Linux.
 - The AWS CLI installed and configured.
 - An Internet browser such as Chrome, Firefox, Safari, or Edge.
 - An AWS account. You will create AWS resources including IAM roles during the workshop.
