# Simple Naming Scheme
> A simple naming scheme for developers.

Having a naming scheme for all resources for a project is a must. This document outlines a simple scheme that seems to work well. Let's converge on something awesome.

## Goals

- readabilty
- sortability
- easily parsable
- expressiveness
- flexibility

Global uniqueness of a name may or may not be important in some cases. Sometimes it's a requirement when using domain names and sometimes it's for convenience. For example, if there are multiple projects with multiple repos in one GitHub account.

## Useful Information

The bits of information (parts) that can be used to name something are:
- company name (ex: acme)
- project name (ex: billing)
- environment or flavor name (ex: stage)
- role name (ex: api)
- index (ex: 1)
- location name (ex: AWS region)

Each part of the constructed name is joined by a separator.
- make sure the separator isn't in any name part if you care to make the resulting grammar non-ambiguous
- if you don't care about parsability (you just want readability) use whatever you like for the separator

The example below uses a colon, but the separator could just as easily be a hyphen.

The scheme looks like this with (in general) least-to-most-specific going left-to-right:

`company:project:environment:role:location:index`

The least-to-most-specific order makes resource names sort together. This is true because normally a specific resource type (ex: AWS security group) will have the same parts specified.

### create a name
```javascript
var separator = ":";
var parts = [ company, project, environment, role, location, index ];
var name  = parts.join(separator);
```

### parse a name
```javascript
var separator = ":";
var part = "([^\s" + escapeRegex(separator) + "]+)?";
var regex = new RegExp([part, part, part, part, part, part].join(separator));
var parts = name.match(regex);
if (parts) {
  console.log("name parts: ", parts.slice(1));
} else {
  console.log("invalid name: ", name);
}
```

**Scenario:**
Acme Corp has a billing service with multiple environments, each in multiple locations.

Here are some example resources and their names (separated by a colon):
- AWS resources
  - EC2 instances
    - `:billing:dev:api::1`
    - `:billing:stage:api::1`
    - `:billing:prod:api::1`
  - S3 buckets
    - `acme:billing:dev:api:us-east-1:`
    - `acme:billing:stage:api:us-east-1:`
    - `acme:billing:prod:api:us-east-1:`
  - Security Groups
    - `:billing:dev:api::`
    - `:billing:stage:api::`
    - `:billing:prod:api::`
- Domains
    - `dev-billing.acme-corp.com`
    - `stage-billing.acme-corp.com`
    - `billing.acme-corp.com`
- Git Repo
  - `acme-billing-api`

Naming domains is simple. For production whatever subdomain you want. For any other environment, just prepend "env-" to the production subdomain! Using this naming scheme for domains actually removes the need to purchase an expensive wildcard cert for a project and each of its environments.

Obviously you can name a Git repo whatever you like. Using the name parts above helps keep things organized.

## Conclusion
The above example is "strict" in that separators are present even when a name part is not specified. You might not want to do this. It's perfectly valid (and prettier) to just use hyphens to separate present parts, when you don't care about being able to parse names. There are usually other identifiers for resources and the name is for a human to understand.

Most projects I have used this naming scheme with actually just use hyphens to separate present parts.
For example: `project-role-us-east-1`

### Collaboration
If there are any questions that need clarification create an issue. If your goal is to improve the naming scheme then please submit a PR!
