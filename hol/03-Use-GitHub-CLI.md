# 🔨 Hands-on: Use GitHub Cli

In this hands-on, we first use the GitHub Cli locally and afterwards create a GitHub workflow which uses the GitHub CLI to create an Issue. 

## Run GitHub CLI locally

> [!IMPORTANT]
> Using the GitHub CLI locally is useful for interacting with the GitHub API in a quick way but it is not mandatory for the second step of this tutorial. If you have unsolvable problems, feel free to skip this step.  

### Install The GitHub CLI
1. Install the GitHub CLI following [this instruction](https://github.com/cli/cli?tab=readme-ov-file#installation)
2. Test the installation by running `gh` in the terminal. 
3. Add autocomplete to your shell following [this instruction]. Test it by entering `gh` plus `tab` in your shell. If everything works, you should see a list of suggestions. 

### Login 
1. Run `gh auth login` in your Terminal. If you are part of GitHub Enterprise, you will be asked which account to login. In that case, choose: `GitHub.com`. Select `SSH` as preferred protocol and select your public ssh key. Lastly select to Login with a browser and follow the instruction in the terminal. 

### Create an Issue
1. Create an Issue with a title and a body in this Repo using the CLI

<details>
  <summary>Solution</summary>
  ```bash
  gh issue create --title "I found a bug" --body "Nothing works" --repo jonath92/ActionsFundamentals
  ```
</details>

## Use GitHub CLI in workflow
 
1. Create a Workflow which can be manually triggered that lists all open issues

<details>
  <summary>Solution</summary>
  
```YAML
name: List issues

on:
  workflow_dispatch: 

jobs:
  list-issues:
    runs-on: ubuntu-latest
    permissions:
      issues: read

    steps:
    - uses: actions/checkout@v4
    - name: List issues
      env:
        GH_TOKEN: ${{ github.token }}
      run: | 
        gh issue list
  ```
</details>

2. Trigger the Worfklow in the Web UI and check the Result
3. Change the Workflow so that the Workflow closes all Issues

> [!HINT]
You can close all issues with: `gh issue list --json number --jq '.[].number' | while read number; do gh issue close $number; done`

<details>
  <summary>Solution</summary>
  
```YAML
name: Close issues

on:
  workflow_dispatch: 

jobs:
  close-issues:
    runs-on: ubuntu-latest
    permissions:
      issues: write

    steps:
    - uses: actions/checkout@v4
    - name: Close issues
      env:
        GH_TOKEN: ${{ github.token }}
      run: | 
        gh issue list --json number --jq '.[].number' | while read number; do gh issue close $number; done
  ```
</details>

## Brainteaser
Imagine you want to extend the workflow to include not only all issues from this repo but from several repos. What steps would be necessary?

## Summary
In this hands-on you've learned how to work with the GitHub CLI both locally and within GitHub Workflows. 
