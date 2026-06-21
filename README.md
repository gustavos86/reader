# GitHub Workflows

Tutorial: [Continuous Integration and Deployment for Python With GitHub Actions](https://realpython.com/github-actions-python/)

There are three main parts that make up the bulk of a workflow file: **triggers**, **jobs**, and **steps**. You’ll cover these in the next sections.

## Workflow Triggers

There are many kinds of triggers:

* Pull request
* Pushed commit to the default branch
* Tagged commit
* Manual trigger
* Request by another workflow
* New issue being opened

Trigger that runs a workflow on any push to the main branch:

```
on:
  push:
    branches:
      - main
```

Official documentation [Events that trigger workflows](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows)

## Workflow Jobs

A workflow can include **one or more jobs** that it will run, and **each job can contain one or more steps**.

Example with no steps:

```
# ...

jobs:
  my_first_job:
    name: My first job
  my_second_job:
    name: My second job
```

You define the runner you want to use to run your job. A runner is a GitHub-hosted virtual machine (VM) that executes your jobs for you.

There are multiple supported operating systems available. You can find the [full list of GitHub-hosted runners](https://docs.github.com/en/actions/concepts/runners/github-hosted-runners#standard-github-hosted-runners-for-public-repositories) in the documentation.

```
# ...

jobs:
  my_first_job:
    name: My first job
    runs-on: ubuntu-latest
    # ...
  my_second_job:
    name: My second job
    runs-on: windows-latest
    # ...
```

## Workflow Steps

Steps are the main part of a job. The steps declare the actions that need to be performed when executing the workflow. This can include tasks such as installing Python, running tests, linting your code, or using another GitHub action.

## GitHub Marketplace

The [GitHub Marketplace](https://github.com/marketplace) is an online repository of all the actions people can use in their own workflows.

## Including Actions in Workflows

1. check out your current repository into the workflow environment
2. install and set up Python

```
# ...

jobs:
  my_first_job:
    name: My first job
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.13"
      - run: python -m pip install -r requirements.txt
```

## Call other Workflows

This line should be on the triggers section

```
workflow_call:
```

Then, call it from another GitHub Workflow

```
# Github-username/repo/path/to/workflow@version
- uses: realpython/reader/.github/workflows/test.yml@master
```

## Tag a commit

```
$ git tag -a "1.0.0" -m "1.0.0"
$ git push --tags
```

## Using secrets in GitHub Actions

[Creating secrets for a repository](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets#creating-secrets-for-a-repository)


## To Puslish

```
Modify version in pyproject.toml
version = "1.1.4"

Commit
git commit -m "Bump version to 1.1.4"

Push with tags
git push origin github-actions-tutorial 1.1.4
```

## Dependabot

[Dependabot options reference](https://docs.github.com/en/code-security/reference/supply-chain-security/dependabot-options-reference)