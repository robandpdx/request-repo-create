# request-repo-create
This repo is used to automate repo creation in a target org using a GitHub Actions workflow.

## Background
As a GitHub Enterprise Admin, you have certian standards for all repos in a target org. These standards may include:
 - repo naming standard
 - branch protection rules
 - standard LICENSE file
 - standard template files (CODEOWNERS, workflows, etc)
 - access via team permissions
 - anything else that [safe-settings](https://github.com/github/safe-settings) can provide

 You simply don't want developer running naked in the streets, creating repos all willy-nilly!!

## Solution
Disable repo creating for all users in the target org. Users requesting a new repo will open an issue in this repo, triggering a GitHub actions workflow that will create a new repo settings file for the requested repo in your [safe-settings](https://github.com/github/safe-settings) admin repo. The new repos settings file is created from a template stored in your [safe-setting](https://github.com/github/safe-settings) admin repo. [Safe-settings](https://github.com/github/safe-settings) will apply the standard rules, configured by the admins for all repos. Upon successul addition of the new repo settings file to the [safe-setting](https://github.com/github/safe-settings) admin repo, the issue will be closed. If [safe-setting](https://github.com/github/safe-settings) is setup and working properly, the new repo will be created according to the new repo settings file.  

## Prerequisites
 - [safe-setting](https://github.com/github/safe-settings) installed and configured in the target org with an admin repo in the target org.
 - Teams defined in the target org.
- GitHub actions runners available for this repo.

## Configuration

You need to define the following secrets in this repo:  
`ADMIN_TOKEN` -  This needs to have write access to the safe-settings admin repo.  

You need to define the following repository varaibles in this repo:  
`TEMPLATE` - The path to the repo settings template file in the admin repo.  
`ORG` - The org where [safe-settings](https://github.com/github/safe-settings) is installed and configured with an admin repo.  
`REGEX` - (Optoinal) A regular expression which the repo names must adhere to. If the repo name does not match this regex, the workflow will fail and a comment will be added to the issue. If this is not defined, no naming restrictions will be applied.  

Customise the [issue template](.github/ISSUE_TEMPLATE/request_repo.yml), editing the teams field as needed. If you are implementing a naming standard for new repos, you should probably detail the standard in the issue template as well.

## Troubleshooting
If the workflow succeeds, but the repo fails to be created, there is likely a failure is [safe-setting](https://github.com/github/safe-settings). Check the [safe-setting](https://github.com/github/safe-settings) logs for more info.  
