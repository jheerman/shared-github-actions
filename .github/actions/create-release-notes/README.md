# Create Release Notes custom action

## Overview
This custom action, can be used, to create release notes on github. It aims to replace the deprecated github release action.
## Usage
Our custom action requires a couple of inputs:
- release
- tag-prefix

**release:** The type of the release. It can be one of the following: `--prerelease`, `--latest`.

**tag-prefix:** The prefix of the tags. It will be used to create the name of the release. We recommend to use the prefix with a dash: `-dev`, `-prod`.

We are using the github cli, to generate the release. You can find more information about the `gh create release` [here](https://cli.github.com/manual/gh_release_create).

## Example
```yaml
      jobs:
      release:
        runs-on: ubuntu-latest
        environment: dev
        permissions:
          id-token: write
          contents: write
        steps:
          - uses: actions/checkout@v4
            with:
              fetch-depth: 0
          - name: Create Release Notes
            uses: jheerman/shared-github-actions/.github/actions/create-release-notes@1.0
            env:
              GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            with:
              release: '--prerelease'
              tag-prefix: '-dev'
```

