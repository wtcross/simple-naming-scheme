# Simple Naming Scheme
> A simple naming scheme for developers.

Having a naming scheme for all resources for a project is a must. This document outlines a simple scheme that seems to work well. Let's converge on something awesome.

Global uniqueness of a name may or may not be important in some cases. Sometimes it's a requirement when using domain names and sometimes it's for convenience. For example, if there are multiple projects with multiple repos in one GitHub account.

The bits of information (parts) that can be used to name something are:
- company name (ex: acme)
- project name (ex: billing)
- environment or flavor name (ex: stage)
- role name (ex: api)
- index (ex: 1)
- location name (ex: AWS region)

The scheme looks like this with (in general) least-to-most-specific going left-to-right:

`company-project-environment-role-location-index`

The least-to-most-specific order makes resource names sort together.

**Scenario:**
Acme Corp has a billing service with multiple environments, each in multiple locations.

Here are some example resources and their names:
- Git repo
  - `acme-billing-api`
- AWS resources
  - EC2 instances
    - `billing-dev-api-1`
    - `billing-stage-api-1`
    - `billing-prod-api-1`
  - S3 buckets
    - `acme-billing-dev-api-us-east-1`
    - `acme-billing-stage-api-us-east-1`
    - `acme-billing-prod-api-us-east-1`
  - Security Groups
    - `billing-dev-api`
    - `billing-stage-api`
    - `billing-prod-api`
- Domains
    - `dev-billing.acme-corp.com`
    - `stage-billing.acme-corp.com`
    - `billing.acme-corp.com`

Using this naming scheme for domains actually removes the need to purchase an expensive wildcard cert for a project and each of its environments.
  
Other than defining each part of the name a separator needs to be picked. Above the separator is a hyphen. If you need to be able to parse names, in logs for example, then take that into consideration when picking the separator.

### Collaboration
If there are any questions that need clarification create an issue. If your goal is to improve the naming scheme then please submit a PR!
