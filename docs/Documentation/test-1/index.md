---
title: test
deprecated: false
hidden: false
metadata:
  robots: index
---
{/*All of the Cloud Asset Compliance calculations are done as part of your discovery cycle using the same AWS accounts that were configured as part of the existing AWS adapters. */}

{/* test */}

## Updated AWS Policy

In order to check all benchmark rules, the AWS policy needs to be updated.

* If you already have an AWS account/role configured in your AWS adapter, you can add [the permissions listed on this page](/docs/aws-permissions#cloud-asset-compliance-permissions) to its AWS policy.

  For details on how to configure AWS Policy, see [Amazon Web Services (AWS) Adapter](/docs/amazon-web-services-aws).

* The following JSON represents the minimum AWS policy required for Cloud Asset Compliance for AWS, which provides Axonius read-only access to resources required for checking all CIS AWS Foundation Benchmark v1.2 rules.
  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "VisualEditor0",
              "Effect": "Allow",
              "Action": [
                  "iam:GenerateCredentialReport",
                  "iam:GetPolicyVersion",
                  "iam:GetAccountPasswordPolicy",
                  "cloudtrail:GetTrailStatus",
                  "s3:GetBucketLogging",
                  "ec2:DescribeFlowLogs",
                  "logs:DescribeMetricFilters",
                  "cloudtrail:GetEventSelectors",
                  "iam:ListVirtualMFADevices",
                  "s3:GetBucketPolicy",
                  "cloudwatch:DescribeAlarmsForMetric",
                  "iam:ListAttachedUserPolicies",
                  "iam:GetCredentialReport",
                  "iam:ListPolicies",
                  "sns:ListSubscriptionsByTopic",
                  "iam:ListEntitiesForPolicy",
                  "iam:ListUserPolicies",
                  "s3:GetBucketAcl",
                  "config:DescribeConfigurationRecorderStatus",
                  "cloudtrail:DescribeTrails",
                  "ec2:DescribeSecurityGroups",
                  "kms:ListKeys",
                  "config:DescribeConfigurationRecorders",
                  "ec2:DescribeVpcs",
                  "iam:ListAccountAliases",
                  "iam:ListUsers",
                  "sts:GetCallerIdentity",
                  "iam:GetAccountSummary",
                  "iam:ListServerCertificates",
                  "access-analyzer:ListAnalyzers",
                  "s3:GetBucketVersioning"
              ],
              "Resource": "*"
          }
      ]
  }
  ```

## Update Advanced Settings to view Affected Assets

The **Affected Assets** displays IAM Users, EC2 machines, and S3 buckets that are affected from AWS entities that failed the check of rules in the CIS benchmarks. In order to display this assets the following must be enabled in the [ Advanced Settings in the AWS Adapter](/docs/amazon-web-services-aws#configuring-aws-correlation-logic-and-retrieved-information):

* Fetch information about IAM Users
* Fetch information about S3

![image.png](https://raw.githubusercontent.com/Axonius/ax-docs-pub/refs/heads/main/Images/image\(1023\)\(836\).png)

Without these settings enabled, you will not be able to see the affected assets in the **Devices/Users** page.