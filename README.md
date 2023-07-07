# Upstream Sync Github Action

Github Action to public upstream repo commits to the private repo.

Forked from gorillio/github-action-sync

## Action

* Pull the upstream
* Get the last commit SHA
* Check if that exists on internal `branch`
* If not, create a pull request

## Inputs

#### `upstream`

**Required** Upstream repo  

#### `upstream_branch`

**Required** Upstream branch to pull from  

#### `branch`

**Required** Branch to merge to  

#### `pr_labels`

Labels for the new PR

## Example usage

```
name: Pull upstream
on:
  schedule:
    # * is a special character in YAML so you have to quote this string
    - cron:  '0 * * * *'
jobs:
  release_pull_request:
    runs-on: ubuntu-latest
    name: release_pull_request
    steps:
    - name: checkout
      uses: actions/checkout@v1
    - name: Create PR to branch
      uses: xascode/github-action-sync@main
      with:
        upstream: ${{ vars.SYNC_UPSTREAM }}
        upstream_branch: ${{ vars.SYNC_UPSTREAM_BRANCH }}
        branch: ${{ vars.SYNC_BRANCH }}
        pr_labels: ${{ VARS_SYNC_LABELS }}
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        GITBOT_EMAIL: ${{ vars.SYNC_EMAIL }}
        DRY_RUN: false
```
