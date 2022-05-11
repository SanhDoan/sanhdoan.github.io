---
title: AWS IAM best practice
author: Sanh Doan
date: 2022-05-12 05:44:00 +0700
categories: [AWS, IAM]
tags: [AWS, IAM]
---

# AWS IAM Section

## Summary

- Users: mapped to a physical user, has a password for AWS console
- Groups: contains users only (can not contain other groups)
- Policies: JSON document that outlines permissions for users or groups
- Roles: for EC2 instances or AWS services
- Security: MFA + Password Policy
- Access Keys: access AWS using the CLI or SDK
- Audit: IAM Credential Reports & IAM Access Advisor

## Best Practices

- Do not use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to group
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication (MFA)
- Create and use Roles for giving permissions ot AWS services
- Use Access Keys for Programmatic Access (CLI/SDK)
- Audit permissions of your account with the IAM Credentials Report
- Never share IAM users & Access Keys

### Q&A, Tips

1. What is a proper definition of an IAM Role?<br/>
   -> An IAM entity thats defines a set of permissions for making requests to AWS services, and will be used by an AWS service

2. IAM Credentials Report is an IAM Security Tool<br/>
   -> IAM Credentials report lists all your AWS Account's IAM Users and the status of their various credentials.

3. IAM Users access AWS services using their own credentials (username & password or Access Keys)

4. Use the root account only to create your first IAM User and a few account/service management tasks. For everyday tasks, use an IAM User.

5. Which principle should you apply regarding IAM Permissions?<br/>
   -> Grant least privilege

6. A statement in an IAM Policy consists of Sid, Effect, Principal, Action, Resource, and Condition. Version is part of the IAM Policy itself, not the statement.
