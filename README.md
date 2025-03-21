# GitHub Action: Run coffeelint with reviewdog 🐶

![Docker Image CI](https://github.com/reviewdog/action-coffeelint/workflows/Docker%20Image%20CI/badge.svg)
[![](https://img.shields.io/github/license/reviewdog/action-coffeelint)](./LICENSE)
[![release](https://github.com/reviewdog/action-coffeelint/workflows/release/badge.svg)](https://github.com/reviewdog/action-coffeelint/actions?query=workflow%3Arelease)
[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/reviewdog/action-coffeelint?logo=github&sort=semver)](https://github.com/reviewdog/action-coffeelint/releases)

This action runs [coffeelint](https://coffeelint.github.io/) with [reviewdog](https://github.com/reviewdog/reviewdog) on pull requests to improve code review experience.

![Example comment made by the action, with github-pr-review](examples/coffeelint-pr-review.png)

## Inputs

**github_token**

**Required**. Default is `${{ github.token }}`.

**level**

Optional. Report level for reviewdog [info,warning,error].
It's same as `-level` flag of reviewdog.

**reporter**

Reporter of reviewdog command [github-pr-check,github-check,github-pr-review].
Default is github-pr-check.
It's same as `-reporter` flag of reviewdog.

github-pr-review can use Markdown and add a link to rule page in reviewdog reports.

**filter_mode**

Optional. Filtering mode for the reviewdog command [added,diff_context,file,nofilter].
Default is added.

**fail_level**

Optional. If set to `none`, always use exit code 0 for reviewdog.
Otherwise, exit code 1 for reviewdog if it finds at least 1 issue with severity greater than or equal to the given level.
Possible values: [`none`, `any`, `info`, `warning`, `error`]
Default is `none`.

**fail_on_error**

Deprecated, use `fail_level` instead.
Optional.  Exit code for reviewdog when errors are found [true,false]
Default is `false`.

**reviewdog_flags**

Optional. Additional reviewdog flags

**coffeelint_flags**

Optional. Flags and args of coffeelint command. Default: '.'

**workdir**

Optional. The directory from which to look for and run coffeelint. Default '.'

## Example usage

You also need to install [coffeelint](https://coffeelint.org).

```sh
# Example
$ npm install coffeelint -D
```

You can create [coffeelint config]() and this action uses that config too.

[.github/workflows/reviewdog.yml](.github/workflows/reviewdog.yml)

```yml
name: reviewdog
on: [pull_request]

jobs:
  coffeelint:
    name: runner / coffeelint
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@50fbc622fc4ef5163becd7fab6573eac35f8462e # v1.2.0
      - name: coffeelint
        uses: reviewdog/action-coffeelint@9499d059575b316fe7facee8f5bb20b10fee3258 # v1.14.2
        with:
          reporter: github-pr-review # Change reporter.
          coffeelint_flags: 'src/'
```
