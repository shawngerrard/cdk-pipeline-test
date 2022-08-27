# cdk-pipeline-test

Implementing pipelines in github actions to test aws cdk iac and aws resource deployments.

# Prerequisites

To use this repository, you must complete the following steps to set up a local aws development environment that utilizes aws cdk.

## Install aws cli

You'll need [aws cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) installed as aws cdk uses aws cli to perform the api calls to the amazon resource model.

## Configure aws cli

Once aws cli is installed, you'll need to [configure it with your default region and access keys](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html), of which you can obtain from your aws account.

## Install iac development language

We'll be utilizing `typescript` to interact with the aws cdk.

To do this, we will need to install the [Node Package Manager](https://www.npmjs.com):
`sudo apt-get install nodejs`

We will also need to install the latest version of [typescript](https://www.typescriptlang.org/):
`npm -g install typescript`

## Install aws cdk

To install the `aws-cdk`, we will use the following command (note that this uses the `global` setting and may require `sudo` priviledges):
`npm install aws-cdk`

You can verify installation with the following command:
`cdk --version`

> **Please note:** Before continuing with the next steps, I recommend configuring a `.gitignore` file to ignore runtime files and pushing this up to your code repository - for instance, exclude the `node_modules` folder that will be created in the next step.

## Install aws cdk libraries

The aws cdk contains language-specific libraries (aws construct library) that organize aws constructs into various modules.

As we'll be utilizing `typescript` to interact with aws cdk, we'll need to install the `aws-cdk-lib` using the node package manager:
`npm install aws-cdk-lib`

## Bootstrap the aws cdk

To use aws cdk we must first bootstrap the cdk app so that required amazon s3 buckets and compute containers can be made available to aws cloudformation during cdk deployment.

As long as you have an aws configuration profile named 'personal' (update the command below if this name differs), we can bootstrap using the following command:
`cdk bootstrap aws://$(aws sts get-caller-identity --o text --query 'Account')/$(aws configure get region --profile personal)`

> **TODO**: Insert a section here describing how to create custom aws lambda execution roles/policies and avoid use of default AdministratorAccess role.
