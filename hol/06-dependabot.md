# 🔨 Hands-on: Use Dependabot
In this hands-on you will learn how to enable dependabot for updating dependencies. 

## Downgrade Github Actions
For Testing purposes make sure that you are using not the most up-to-date version for all github actions. You could for example change the `actions/checkout` version to Version 3. 

## Enable Dependabot
1. Follow the steps described [here](https://docs.github.com/en/code-security/getting-started/dependabot-quickstart-guide#enabling-dependabot-for-your-repository). Also do the 5th step which creates a `dependabot.yml` file for you. For the `package-ecosystem` use: `github-actions` and commit the file to the main branch.  

2. Go to the `Actions` Tab and you should see a `Dependabot Update` Workflow and a run. Wait until the Run is done. 

3. Go to the `Pull requests` Tab and review the Open Pull Requests. Important: Don't merge it yet when you want to test the *Enable Auto-Merge* Feature


## Enable Auto-Merge
1. If you want to enable auto-merge, you can do so by creating another GitHub Workflow: 

<details>
  <summary>Solution</summary>

```yaml 
name: Dependabot auto-merge
on:
  - pull_request

permissions:
  contents: write
  pull-requests: write

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - name: Dependabot metadata
        id: metadata
        uses: dependabot/fetch-metadata@v2
        with:
          github-token: "${{ secrets.GITHUB_TOKEN }}"
      - name: Enable auto-merge for Dependabot PRs
        run: gh pr merge --auto --squash "$PR_URL"
        env:
          PR_URL: ${{github.event.pull_request.html_url}}
          GH_TOKEN: ${{secrets.GITHUB_TOKEN}}
```
</details>

2. Retrigger Dependabot update by closing the pull request with the comment: `@dependabot reopen`. Dependabot should now automatically reopen the pull request and the Auto-Merge Workflow should be triggered. 


## View Dependabot Run

## Set Dependabot for Github Actions
