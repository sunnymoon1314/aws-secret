# Managing secrets and parameters in AWS

You may be wondering how you can store and retrieve both secrets and variables in AWS which may be necessary in your CI/CD pipelines.

## What are the differences between secrets and variables?
### Secrets:
- Purpose: Secrets are sensitive data like API tokens, access keys, and credentials that you don't want to expose in your workflow files or logs.
- Storage: Encrypted and stored as secrets within the repository settings.
- Usage: Commonly used for sensitive data needed during workflow execution, like access tokens for external services or credentials.
- Visibility: Hidden in logs unless explicitly used in actions/steps.

For this, we can store secrets in AWS Secrets Manager

### Variables:

- Purpose: Variables are general-purpose values stored within GitHub Actions and can include strings, integers, or other data types.
- Storage: Stored as environment variables or repository environment variables.
- Usage: Used to set up workflow behavior, store commonly used values, or configure aspects of workflows.
- Visibility: Environment variables can be visible in logs unless marked as secrets.

For this, we can store secrets in AWS Parameter Store

## AWS Secrets Manager
![image](https://github.com/luqmannnn/aws-secret/assets/9068525/ac5eda26-e5a7-4fe5-9cdc-de23ca5ec925)
AWS Secrets Manager helps you manage, retrieve, and rotate database credentials, API keys, and other secrets throughout their lifecycles. 

## AWS Systems Manager Parameter Store
Parameter Store, a capability of AWS Systems Manager, provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, Amazon Machine Image (AMI) IDs, and license codes as parameter values. You can store values as plain text or encrypted data. You can reference Systems Manager parameters in your scripts, commands, SSM documents, and configuration and automation workflows by using the unique name that you specified when you created the parameter. 

Parameter Store is also integrated with Secrets Manager. You can retrieve Secrets Manager secrets when using other AWS services that already support references to Parameter Store parameters. 

Useful link: https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-working-with.html

## Getting Started

### AWS Secrets Manager
1. In your console, go to AWS Secrets Manager
2. Click "Store a new secret"
3. Choose the type of secret you would like to store e.g. "Other type of secret"
4. Enter the secret key and value pair you would like to store. You may add multiple of this.
5. Next, give your secret a name e.g. prod/database/mysql
6. Next, you can also optionally choose whether you'd like automatic secret rotation. Secret rotation is the practice of generating new secrets after a stipulated period of time to ensure better security.
7. Create your secret.
8. In Github, you can retrieve the secret by running a command like: ```secret_object=$(aws secretsmanager get-secret-value --secret-id prod/database/mysql --query SecretString --output json)```

### AWS Systems Manager Parameter Store
1. In your console, go to AWS Systems Manager > Parameter Store
2. Click "Create parameter"
3. Give your parameter a name and value e.g. "app_name" with Data type = "String" and Value = "mysql_db_webapp"
4. Create parameter.
5. In Github, you can retrieve the secret by running a command like: ```parameter_value=$(aws ssm get-parameter --name app_name --query Parameter.Value --output text)```
"# aws-secret" 
