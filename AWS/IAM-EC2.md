# IAM and EC2 AWS Introduction

## IAM Introduction

- IAM stands for Identity and Access Management
- all of your aws security is in your IAM
  - this includes users, groups, and roles
- Your root account should never be used or shared
- Users myst be created with the permisions you want them to have
- IAM is the control center of AWS
- Policies are written in JSON
- IAM has a global view
  - this means that it applies to all of your applications
- MFA can be set up (Multi Factor Authentication)

## Users

- a physical person who is in your organization
- One IAM User per Physical Person
- Never share IAM credentials
- **Never use the Root Account except for initial setup**
- **Never use Root IAM credentials**

## Groups

- a way of organizing your users by their function (admins, devops) and teams (engineering, design). contains users

## Roles

- Internal useage within AWS resources
- usually given to machines to do stuff
- one IAM role per application

## Policices

- Written in JSON Documents
- defines what each user, group and role can and can not do
- IAM has predefined "managed policies"
- IT is bst practice to give users the minimal ammount of permission they need to do their job. For security. least privilege principle

## IAM Federation

- Big enterprises use this to integrate their own repositioty of susers with IAM
- This allows users to log into aws using their own company credentials
- identity Federation uses the SAML standard (Active Directory)
