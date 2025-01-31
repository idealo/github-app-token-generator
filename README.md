# Deprecation Notice ⚠️
**This repository is no longer maintained.**  
We recommend switching to the official GitHub repository for the Create GitHub App Token action.  
- Official Repository: https://github.com/actions/create-github-app-token  
- Recommended Action: Update your GitHub workflows to use the official action.  

Please update your workflow files to use the latest version of the official action to ensure you have the most up-to-date features, security patches, and support.
### Migration Steps  
1. Replace the current action reference with the official one
2. Review the documentation in the official repository
3. Test your workflows to ensure compatibility  

Example Migration:
```
- uses: actions/create-github-app-token@v1
  id: app-token
  with:
  app-id: ${{ vars.APP_ID }}
  private-key: ${{ secrets.PRIVATE_KEY }}
  owner: ${{ github.repository_owner }}
```

# GitHub App installation access token generator

GitHub Action that can be used to generate an installation access token for a GitHub App. This token can for instance be used to clone repos, given the GitHub App has sufficient permissions to do so.

## Usage

```yaml
name: Checkout repos
on: push
jobs:
  checkout:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - uses: idealo/github-app-token-generator@v1.0.0
      id: get-token
      with:
        private-key: ${{ secrets.IDEALO_BOT_GH_APP_PRIVATE_KEY }}
        app-id: ${{ secrets.IDEALO_BOT_GH_APP_ID }}

    - name: Check out an other repo
      uses: actions/checkout@v2
      with:
        repository: owner/repo
        token: ${{ steps.get-token.outputs.token }}
```

## Requirements

The action needs two input parameters, `private-key` and `app-id`. To get these, simply create a GitHub App. The private key can be generated and downloaded, and should be added to the repos as a secret.

The installation ID that is used during the creation of the access token is created against the repo running the action. If you need to create the installation ID for a different repo you can use the `repo` input:

```yaml
uses: idealo/github-app-token-generator@v1.0.0
id: get-token
with:
  private-key: ${{ secrets.IDEALO_BOT_GH_APP_PRIVATE_KEY }}
  app-id: ${{ secrets.IDEALO_BOT_GH_APP_ID }}
  repo: some/repo
```
