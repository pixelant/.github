# Contributing

Welcome, and thank you for your interest in contributing

As a contributor, here are the guidelines we would like you to follow:

- [Questions and Support](#if-you-have-a-question-or-need-a-support)
- [Bug Report](#add-a-bug-report)
- [Feature Requests](#add-a-new-feature)
- [Submission Guidelines](#submission-guidelines)
- [Coding Guidelines](#coding-guidelines)
- [Browsers and Devices](#browsers-and-devices)
- [Code of Conduct](#code-of-conduct)

***

## ❓If you have a question or need a Support

Do not open issues for general support questions as we want to keep **GitHub issues** for bug reports and feature requests. [Slack channel](SUPPORT.md) is a much better place to ask questions and get support.

To save your and our time, **we will regularly close all issues** that are requests for general support and redirect people to Slack.

## 🐞Add a Bug report

If you find a bug in the code or a mistake in the documentation, you can help us by [submitting an issue](#submitting-an-issue) to particular repository, or even better, you can [submit a Pull Request](#submitting-a-pull-request) with a fix.

## 🚀Add a new Feature

You can request a new feature by submitting an issue to our repository. If you would like to implement a new feature, please submit an issue with a proposal for your work first, to be sure that we can use it. Please consider what kind of change it is:

- For a **Major Feature**, first open an issue and outline your proposal so that it can be discussed. This will also allow us to better coordinate our efforts, prevent duplication of work, and help you to craft the change so that it is successfully accepted into the project.
- **Small Features** can be crafted and directly submitted as a Pull Request.

***

## Submission Guidelines

### Submitting an Issue

Before you submit an issue please check that you've considered the following steps:

- Add a single issue per problem
- Check **duplicates** - use the search feature to ensure that the problem hasn't been reported before.
- Check **dependencies** - make sure you're on the right version of dependencies.
- Check [Browsers and devices](#browsers-and-devices)
- Use **Issue templates** - add a new issue by filling out the issue template.

Unfortunately, we are not able to investigate/fix bugs without a minimal reproduction, so if we don't hear back from you **we are going to close an issue** that doesn't have enough info to be reproduced.

### Submitting a Pull Request

Before you submit your Pull Request (PR) please check that you've considered the following steps:

- ❗️**Please ask** first before embarking on any significant pull request, otherwise you risk spending a lot of time working on something that the project's developers might not want to merge into the project. [Create an Issue](#submitting_an_issue) to discuss potential big PR.
- Search in GitHub for an open or closed Pull Request that relates to your submission.
- Provide plenty of context and reasoning around your changes, to help us merge quickly.
- Follow our [Coding Rules](#coding-rules)
- Follow our [Commit message conventions](#commit-message-guidelines)
- Close related issue in PR header message using [GitHub keywords](https://help.github.com/articles/closing-issues-via-commit-messages).
- If your PR gets out of date, we may ask you to rebase as you are more familiar with your changes than we will be.
- If your PR fail on CI tests, we may ask you to fix it.
- [Check documentation about Pull Request on Github](https://help.github.com/articles/using-pull-requests)

***

## Coding Guidelines

❗️ This part is quite important. If some of these rules are missed, you will not pass the CI test and will not be able to contribute. This is not to add complexity, but to maintain the quality of the code at a good level in the long run.

***

### 1. Make sure that you have the correct required dependencies

### 2. Code style

#### Editor config

- Set your editor to use **Editor config** settings to avoid common code inconsistencies and dirty diffs. _[Read more about Editor config and download plugins](https://editorconfig.org)_

```
# This file is for unifying the coding style for different editors and IDEs
# editorconfig.org

root = true

[*]
charset = utf-8
# Get rid of whitespace to avoid diffs with a bunch of EOL changes
trim_trailing_whitespace = true
# Unix-style newlines with a newline ending every file
end_of_line = lf
insert_final_newline = true
indent_style = space
indent_size = 4

# TypeScript/JavaScript/JSON files
[*.{ts,js,json}]
indent_size = 2

# TypoScript/TSconfig files
[*.{typoscript,tsconfig}]
indent_size = 2

# XLF/XML files
[*.{xlf,xml}]
indent_style = tab

# YAML-Files
[*.{yaml,yml}]
indent_size = 2

# ReST-Files
[*.rst]
indent_size = 3

# SQL files
[*.sql]
indent_style = tab
indent_size = 2

# .htaccess
[{_.htaccess,.htaccess}]
indent_style = tab

# HTML files
[*.html]
indent_size = 2

# CSS/SCSS files
[*.{css,scss}]
indent_size = 2
```
#### PHP

- We follow [TYPO3 coding guidelines](https://docs.typo3.org/m/typo3/reference-coreapi/master/en-us/CodingGuidelines/Index.html) plus `.phpcs.xml`

`.phpcs.xml`
```
<?xml version="1.0"?>
<ruleset name="pixelant">
	<rule ref="PSR2"/>
	<rule ref="Generic.Files.LineLength">
		<properties>
			<property name="lineLimit" value="160"/>
			<property name="absoluteLineLimit" value="170"/>
		</properties>
	</rule>
	<file>...</file>
</ruleset>
```
#### TypoScript
`typoscript-lint.yml`
```
paths:
  - Configuration/TypoScript/
  - Configuration/TSconfig/

sniffs:
  - class: Indentation
    parameters:
      indentPerLevel: 2
  - class: RepeatingRValue
    disabled: true
  - class: DeadCode
    disabled: true
  - class: NestingConsistency
    parameters:
      commonPathPrefixThreshold: 3
```

#### JS

- We follow [JavaScript Standard Style](https://standardjs.com)

#### CSS

- We follow [Stylelint Config Standard](https://github.com/stylelint/stylelint-config-standard) with some adjustments:

``` json
    "plugins": [
      "stylelint-no-unsupported-browser-features"
    ],
    "rules": {
      "selector-pseudo-element-colon-notation": "single",
      "no-descending-specificity": null,
      "comment-empty-line-before": null,
      "at-rule-no-unknown": null,
      "plugin/no-unsupported-browser-features": true
    }
```

#### Shell scripts

- Use [shellcheck](https://github.com/koalaman/shellcheck) static analysis tool for shell scripts

#### Dockerfile

- Use [hadolint](https://github.com/hadolint/hadolint) as a Dockerfile linter

***

### 3. GIT

#### Commit Message Guidelines

- Each commit message consists of a **[label](#labels)** and short **[message](#git-message)**. Also, it is possible to use special keywords for [closing Github issues](https://help.github.com/articles/closing-issues-via-commit-messages).

#### Git message

- Use the imperative, present tense: "change" not "changed" or "changes"
- don't capitalize the first letter
- no dot (.) at the end

#### Labels

- Please use semantic labels for your messages, but if commit message is not very important, you can skip the label.
- ❗️**Only commit with label will be added in CHANGELOG file**, that's why it is important to use predefined labels on your commits.

    - **[FEATURE]** - A new feature
    - **[BUGFIX]** - A bug fix
    - **[TASK]** - Any task, which is not a **new feature** or **bugfix**
    - **[TEST]** - Adding/updating tests and CI config
    - **[DOC]** - Documentation only changes/updates
    - **[WIP]** - Work in progress tag, should not be present when creating pull requests
    - **[!!!]** - Breaking Changes

- ❗️**Important:** Commit label must be **only one**, except if it Breaking Changes, then we will need to add _"Breaking Changes"_ label `[!!!]` at front.

    - For example (Breaking Change):

    ``` git
        [!!!][BUGFIX] change default CSS styling for Text and Image CE
    ```

***

## Browsers and Devices

We support the **latest and popular browser versions** of each major mobile and desktop platforms. 

We are using [Can I Use](https://caniuse.com/usage-table) data and [Browserslist](https://github.com/browserslist/browserslist) plugin to manage and define the target browsers list

- Check `package.json -> browserslist` where you can always find an up-to-date list of supported browsers

***

## Code of Conduct

This project has a [Code of Conduct](CODE_OF_CONDUCT.md). By interacting with this repository, organization, or community you agree to abide by its terms.
