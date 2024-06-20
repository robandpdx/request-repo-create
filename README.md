# request-repo-create
This repo is used to automate repo creation in a target org using a GitHub Actions workflow.

## Background
As a GitHub Enterprise Admin, you have certian standards for all repos in a target org. These standards may include:
 - repo naming standard
 - standard LICENSE file
 - standard template files (CODEOWNERS, workflows, etc)
 - access via team permissions

 You simply don't want developer running naked in the streets, creating repos all willy-nilly!!

## Solution
Disable repo creating for all users in the target org. Users requesting a new repo will open an issue in this repo, triggering a GitHub actions workflow that will create a new repo. Upon successul repo creation, the issue will be closed.  

## Prerequisites
- Teams defined in the target org.
- GitHub actions runners available for this repo.

## Configuration

You need to define the following secrets in this repo:  
`ADMIN_TOKEN` -  This needs to have write access to the org where the new repos will be created.  

You need to define the following repository varaibles in this repo:  
`ORG` - The org where where the new repos will be created.  
`ADMIN_TEAM` - The team in the target org that has admin access to the new repo.  
`REGEX` - (Optional) A regular expression which the repo names must adhere to. If the repo name does not match this regex, the workflow will fail and a comment will be added to the issue. If this is not defined, no naming restrictions will be applied.  
`TEMPLATE` - (Optional) The name of a template repo to create the new repos from.  
`VISIBILITY` - The visibility of the new repo. Can be `private`, `public`, or `internal`. If this is not defined, the new repo will be private.

Customise the [issue template](.github/ISSUE_TEMPLATE/request_repo.yml), editing the teams field as needed. If you are implementing a naming standard for new repos, you should probably detail the standard in the issue template as well.
