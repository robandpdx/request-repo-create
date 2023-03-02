# request-repo-create
This repo is used to automate repo creation for an org using a GitHub Actions workflow.

## Background
As a GitHub Enterprise Admin, you have certian standards for all repos. These standards may include:
 - a repo naming convention
 - branch protection rules
 - a standard LICENSE file
 - a standard template files (CODEOWNERS, workflows, etc)
 - access via team permissions
 - anything else that [safe-settings](https://github.com/github/safe-settings) can provide

## Solution
Users open an issue in this repo, triggering a GitHub actions workflow that will create a new repo settings file for the requested repo in your [safe-settings](https://github.com/github/safe-settings) admin repo. The new repos settings file is created from a template stored in your [safe-setting](https://github.com/github/safe-settings) admin repo. [Safe-settings](https://github.com/github/safe-settings) will apply the standard rules, configured by the admins for all repos. Upon successul addition of the new repo settings file to the [safe-setting](https://github.com/github/safe-settings) admin repo, the issue will be closed.  

## Prerequisites
 - [safe-setting](https://github.com/github/safe-settings) installed and configured with an admin repo in the org
 - GitHub actions runners available
 - Teams defined in your org

## Configuration

You need to define the following secrets in this repo:
`ADMIN_TOKEN` -  This needs to have write access to the safe-settings admin repo.  

You need to define the following repository varaible in this repo:  
`TEMPLATE` - The path to the repo settings template file in the admin repo.  
`ORG` - The org where [safe-settings](https://github.com/github/safe-settings) is installed and configured with an admin repo.  
`REGEX` - A regular expression which the repo names must adhere to. If the repo name does not match this regex, the workflow will fail and a comment will be added to the issue. If this is not defined, no restrictions will be applied.  

Customise the issue template, adding teams as needed.

## Troubleshooting
The the workflow succeeds, but the repo fails to be created, there is likely a failure is [safe-setting](https://github.com/github/safe-settings). Check the [safe-setting](https://github.com/github/safe-settings) logs for more info.  
