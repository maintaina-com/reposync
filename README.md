# reposync

This repository holds a Github Actions workflow that regularly pulls in changes
from Horde upstream and rebases Maintaina's forked packages onto the changes.

## Workflow Triggers

The workflow has two triggers: It runs automatically every Tuesday at 00:00 UTC
or can be started manually if required. For manual execution, you need to be logged into Github as a member of maintaina-com. The button to start the workflow can then be found, if you navigate to the Actions tab and then select the rebase workflow on the left side.

## Workflow Steps

Per forked Horde package, the following steps are executed in the workflow:

- rebase horde-upstream branch on horde upstream repo
- rebase maintaina-bare on horde-upstream, abort on conflicts
- recreate maintaina-composerfixed based on maintaina-bare
- generate a new composer.json on that branch
- rebase master branch on maintaina-composerfixed

## Workflow Matrix

## How to add/remove packages from reposync

Simply edit the package list in `.github/workflows/rebase-onto-upstream.yml`, below
the `matrix` keyword.

## Excluded Repositories

The workflow does not sync all repositories of maintaina-com. Repositories,
that do not have a Horde upstream are excluded by default. Of the forked
repositories, there are some excluded as well:

- still need some preparations:
    - contents
    - Controller
    - Dav
    - Test
- does not have a .horde.yml:
    - git-tools
    - horde-deployment
    - horde-installer-plugin
    - Model
    - pear-core
    - ReflectionDocBlock
    - Text_Wiki
