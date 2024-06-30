# 🔨 Hands-on: Use GitHub Cli

In this hands-on, we first use the GitHub Cli locally and afterwards create a GitHub workflow which uses the GitHub CLI to create an Issue. 

## Run GitHub CLI locally

> [!IMPORTANT]
> Using the GitHub CLI locally is useful for interacting with the GitHub API in an easy way but it is not mandatory for the second step of this tutorial. If you have unsolvable problems, feel free to skip this step.  

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
  gh issue create --title "I found a bug" --body "Nothing works" --repo jonath92/ActionsFundamentals
</details>

## Use GitHub CLI in workflow
 
1. Create a Workflow which can be manually triggered that lists all open issues and logs them to the Workflow Log



