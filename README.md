# SNS Email Topic Terraform Module #

## Introduction

Although Terraform supports most of the AWS SNS resource options you'll need
sometimes you'll want to set up a notification topic that uses the email or
email-json protocols. When using either of those an email is sent to the given
address that needs to be confirmed out of bounds, which isn't really the model
that Terraform wants, or should, support.

This thin wrapper module creates an SNS email topic using a tiny CloudFormation
stack and exposes the topics ARN back to, and through, Terraform

## Usage

Use the module in your terraform files:

    module "admin-sns-email-topic" {
        source = "github.com/deanwilson/tf_sns_email"

        display_name  = "Example.org Admin Notifications"
        email_address = "admin@example.org"
        owner         = "Example.org:Admin"
        stack_name    = "admin-sns-email"
    }

and then run a `terraform get` to download the module.

Once you've applied it you can check the value with

    terraform output -module=admin-sns-email-topic arn

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| aws_region | AWS region | string | `eu-west-1` | no |
| display_name | Name shown in confirmation emails | string | `tf_sns_email` | no |
| email_address | Email address to send notifications to | string | `` | no |
| owner | Sets the owner tag on the CloudFormation stack | string | `tf_sns_email` | no |
| protocol | SNS Protocol to use. email or email-json | string | `email` | no |
| stack_name | Cloudformation stack name that wraps the SNS topic. Must be unique. | string | `tf_sns_email` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | Email SNS topic ARN |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->


### TODO

 * Find a way to pass an arbitrary mapping of tags through to the cfn stack.

### Author

  [Dean Wilson](http://www.unixdaemon.net)
