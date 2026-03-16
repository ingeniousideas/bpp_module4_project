# Readme for Module 4 Project Cloud

## [Contents](#contents)

- [Objective](#objective)
  - [Architecture](#architecture)
  - [Networking](#networking)
- [MVP](#mvp)
  - [MVP Components](#mvp---components)

## [Objective](#contents)

Build at least a three tier web application on AWS. Developed in **AWS Academy Learner Lab** environment.

### [Architecture](#contents)

- Web served front-end.
- Backend logic processing layer.
- Data persistence layer.
  - This could be PaaS database.
  - Thinking likely MySQL since only a simple small app.

Need to demonstrate wrap-around features such as Security (BIG DEAL), Monitoring and Cost.

### [Networking](#contents)

Big emphasis on five rules of networking:

1. Redundancy.
2. Scaleability.
3. Security.
4. Manageability.
5. Functionality.

## [MVP](#contents)

Try build MVP with **AWS Lab Project**. Replicate the work done here in **AWS Academy Learner Lab**. Where insufficient knowledge or understanding, dip into **AWS Academy Cloud Developing**.

### [MVP - Components](#contents)

High level components for MVP for TradeStream.

## [Documentation and References](#contents)

Document everything here. To use as primer/draft for video presentation.

### [Presentation Artefacts](#contents)

- [**AWS Learner Lab Project**](/AWS_Learner_Lab_Project.md) key document.
  - Notes of AWS development.
  - Mermaid diagrams.
  - draw.io diagrams.
  - Discussion notes and bullet lists.

### [Video on YouTube](#contents)

- 20 minutes.
  - Link added to submission.
- AWS SDK CLI Commands used to build and create resources.
- Reasoning behind choices, as indicated in **AWS Lab Project**.

## [North Star](#contents)

Additional components and configuration etc that might be included for a North Star implementation.

### [Use CloudFormation](#contents)

Develop a CloudFormation Template in JSON

- Follows ecma json standards
- YAML v1.1 specification with a few exceptions.
  - Does not support:
    - Binary omap
    - pairs
    - sets
    - timestamp tags
    - aliases
    - hash merges

Template and CloudFormation creates a "Stack" of resources.

Resources limited by quota.

Templates create documentation of infrastructure.

#### [Example CloudFormation template structure](#contents)

From <https://awsacademy.instructure.com/courses/157153/modules/items/15336803>

```json
{
  "AWSTemplateFormatVersion" : "version date, 2020-09-09 is latest??",
  "Description" : "JSON string",
  "Metadata" : {template metadata},
  "Parameters" : {set of parameters},
  "Mappings" : {set of ... Similar to look-up able},
  "Conditions" : {set of ... Whether resources created, or resrouces properties applied during creation or update. Could depend on whether dev or prod},
  "Transform" : {set of ...for serverless apps, Lambda, which AWS SAM to use.},
  "Resources" : {set of ...Stack resources and properties. EC2 instance, bucket},
  "Outputs" : {set of ...values returned whenever view stacks properties. Can sue depndes on to order creation.}
}

```

#### [Detailed Section Examples](#contents)

Example description:

```json
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "AWS CloudFormation Sample Template ElasticBeanstalk_Simple: Configure and launch an Elastic Beanstalk application that connects to an Amazon RDS database instance. Monitoring is set up on the database.",
  "Parameters": {
    "DBUser": {
      "NoEcho": "true",
      "Type": "string",
      "Description": "Test database admin account name"
    }
  }
}
```

Example Parameters section:

```json
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "AWS CloudFormation Sample Template Config: This template demonstrates the use of AWS Config parameters.",
  "Parameters": {
    "Ec2VolumeAutoEnableIO": {
      "Type": "String",
      "Default": "false",
      "AllowedValues": ["false", "true"]
    }
  }
}
```

Resources Section (Required):

```json
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "AWS CloudFormation Sample Template Config: This template demonstrates the use of AWS Config resources.",

  "Resources": {
    "Ec2Volume": {
      "Type": "AWS::EC2::Volume",
      "Properties": {
        "AutoEnableIO": {"Ref": "Ec2VolumeAutoEnableIO"},
        "Size": "5",
        "AvailabilityZone": {"Fn::Select": [0,{"Fn::GetAZs": ""}]},
        "Tags": [{
            "Key": {"Ref": "Ec2VolumeTagKey"},
            "Value": "Ec2VolumeTagValue"
          }]
      }
    }
  }
}
```
