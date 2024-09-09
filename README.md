# GitHub Action: Post [appsharing.space](https://appsharing.space) link to PR

## What is it
A GitHub Action that posts comments to a pull request with the preview link of a workflow artifact using [appsharing.space](https://appsharing.space).


## Features
- Automatically generate the appsharing.space link with workflow artifact.
- Post a comment on the associated PR using the link.

## Usage
Here is an example of using this action. It is triggered at the end of a successful workflow and it needs the PR `write` permission to post comments.
 

```yaml
name: Comment link to the pull request
on:
  workflow_run:
    workflows: [<YOUR WORKFLOW NAME>]
    types:
      - completed
permissions:
  pull-requests: write

jobs:
  comment:
    runs-on: ubuntu-latest
    if: >
      ${{ github.event.workflow_run.event == 'pull_request' &&
      github.event.workflow_run.conclusion == 'success' }}
    steps:
      - name: "Comment APSS link on PR"
        uses: trungleduc/appsharingspace-pr-comment/.github/actions/pr-comment@v1
        with:
          artifact_name: my-artifact
          index_path: dist/index.html
          comment_prefix: **PR preview link: **
          
```

## Input
- `artifact_name`: name of the artifact file, default to `artifact`
- `index_path`: path to the main index.html file, default to `index.html`
- `comment_prefix`: message before the link, default to `**Preview PR at**`

