# Simple Naming Scheme
> A simple naming scheme for developers.

Having a naming scheme for all resources for a project is a must. This document outlines a simple scheme that seems to work well.

Global uniqueness of a name may or may not be important in some cases. Sometimes it's a requirement when using domain names and sometimes it's for convenience. For example, if there are multiple projects with multiple repos in one GitHub account.

The bits of information (parts) that can be used to name something are:
- project name (ex: acme)
- sub-project name (ex: billing)
- role name (ex: api)
- environment or flavor name (ex: stage)
- location name (ex: AWS region)

**Scenario:**
Acme Corp has a billing service with multiple environments, each in multiple locations.

Here are some example resources and their names:
- Git repo
  - `acme-billing-api`
- AWS resources
  - EC2 instances
    - `billing-api-dev`
    - `billing-api-stage`
    - `billing-api-prod`
  - S3 buckets
    - `acme-billing-api-dev-us-east-1`
    - `acme-billing-api-stage-us-east-1`
    - `acme-billing-api-prod-us-east-1`
  - Security Groups
    - `billing-api-dev`
    - `billing-api-stage`
    - `billing-api-prod`
- Domains
    - `dev-billing.acme-corp.com`
    - `stage-billing.acme-corp.com`
    - `billing.acme-corp.com`
  
Each name part is separated by some separator. Since I don't need to parse names I just use "-" as the separator in the examples above. If you want to be able to parse the names above in an easy way then don't use "-" in name parts.
