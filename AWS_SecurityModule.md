# Review of the Security Module

What can be learnt and applied from this module.

## Shared Responsibility Model

AWS - Security of the cloud:

- Physical security of data centres
- Hardware and software infra

Us responsible for in the cloud. Using tools. Encryption, network security, credentials

- OS on EC2
Security Groups
Apps passwords

## IAM

- users
- groups
- roles

- IAM User
  - Person
- IAM Group
  - Access Policies
  - Groups of individuals
- Policies
  - Defines which resources can eb accessed and level of access
  - Can be attached to IAm User or IAM Group
- IAM Role
  - Temp set of permissions for making AWS service requests
  - Similar to invoking sudo for particular activity

Programmatic access
AWS Management Console Access.

### Use of IAM Role

- Create an IAM Policy that specifies which resources can be accessed.
- Assign this Policy to an IAM Role.
- Allow specific application e.g. one or more microservice, to use IAM Role to access resource, that may be to request data from History Microservice, or execute Sentiment Analysis etc.
