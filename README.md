# AWS Cloud Cost Optimization - Identifying Stale Resources

## Identifying Stale EBS Snapshots

In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

### Description:

The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

## Diagram

![](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Cloud-Cost/Cost-Optimization.png?raw=true)

## Screenshots

#### **1. Testing with an Active EC2 Instance**

_Result_: The Lambda function does not delete EBS snapshots associated with active EC2 instances.

![Active](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Cloud-Cost/Running.png?raw=true)

#### **2. Testing After Deleting EC2 Instance**

_Result_: The Lambda function successfully deletes the EBS snapshots associated with the deleted EC2 instance.

![](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Cloud-Cost/Delete.png?raw=true)

## Live Demo

## Table of Contents

1.  [Overview](#overview)
2.  [Features](#features)
3.  [Tech Stack](#tech-stack)
4.  [What I Learned](#what-i-learned)
5.  [How It Works](#how-it-works)
6.  [Usage](#usage)
7.  [Setup and Deployment](#setup-and-deployment)
    - [Prerequisites](#prerequisites)
    - [IAM Role and Policy](#iam-role-and-policy)
8.  [Future Improvements](#future-improvements)

## Overview

This project focuses on optimizing AWS cloud costs by identifying and removing stale resources, specifically unused EBS snapshots. Snapshots often accumulate over time, consuming unnecessary storage costs. Automating the identification and cleanup process helps optimize your cloud infrastructure efficiently.

This solution utilizes an AWS Lambda function that identifies EBS snapshots no longer associated with any active EC2 instance and deletes them. The automation ensures cost savings while maintaining efficient resource utilization.

## Features

- Automates identification of stale EBS snapshots.
- Deletes snapshots no longer associated with active EC2 instances.
- Reduces AWS storage costs by removing unused resources.
- Configurable and easy to integrate into existing AWS accounts.

## Tech Stack

- **AWS Lambda**: Serverless computing platform to run the cleanup function.
- **Python**: Scripting language used to implement the Lambda function.
- **EC2**: Compute service for hosting and managing virtual machines.
- **EBS Snapshots**: Point-in-time copies of EBS volumes for backup and recovery.
- **IAM**: Custom roles and policies to securely access AWS services.

## What I Learned

1.  **Understanding AWS Services**:
    - Gained in-depth knowledge of AWS EC2, EBS snapshots, and IAM policies.
2.  **Automation with AWS Lambda**:
    - Learned to use AWS Lambda for automating cleanup tasks and optimizing costs.
3.  **Debugging and Testing**:
    - Understood how to debug and test AWS Lambda functions using manual triggers and logs in CloudWatch.

## How It Works

1. **Fetch EBS Snapshots**: The Lambda function fetches all snapshots owned by the account.
2. **Retrieve Active EC2 Instances**: A list of active EC2 instances (running or stopped) is retrieved.
3. **Identify Stale Snapshots**: Snapshots whose associated volumes are not attached to any active instances are marked as stale.
4. **Delete Stale Snapshots**: The function deletes these snapshots to free up storage.

## Usage

- **Triggering Lambda**: Use AWS EventBridge or schedule the Lambda function to run periodically.
- **Monitoring**: Use AWS CloudWatch logs to monitor the Lambda function execution and verify deleted snapshots.

## Setup and Deployment

### Prerequisites

- AWS Account with access to Lambda, EC2, and EBS services.
- Python installed locally for testing.
- IAM user/role with appropriate permissions.

### IAM Role and Policy

- Role created by Lambda Function

![](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Cloud-Cost/Role.png?raw=true)

- Create Custome Policy

![](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Cloud-Cost/Policy.png?raw=true)

**Note:-** Attach the custom policy to the Role( That created by Lambda)
