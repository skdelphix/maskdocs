# Welcome to the New Face of Delphix Masking Documentation

Delphix Masking is embarking on a great-- nay, a noble quest. It is a quest to break the shackles of Confluence once and for all, and usher in an era of prosperity and great documentation... with Markdown.

## Installation

Please have a look through the following requirements and steps. If you're impatient and want to just run quick commands to get it done, scroll to [Quick Steps](#quick-steps)

### Clone this repo

Open your terminal, ```cd``` to whatever top level directory you want and paste:

`git clone git@gitlab.delphix.com:docs/docsdev.git`

Now we need to get Python 3 installed. If you already have it installed, you can skip ahead to [Install pipenv](#install-pipenv). If you are a savvy adventurer in Pythonland and already have `pipenv` installed, skip to [Set up your environment](#set-up-your-environment).

### Install Python 3

The fastest way to do this on OSX is to install Homebrew and use it to install python3.

1. Install homebrew if it's not already installed: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

2. Update homebrew: `brew update`

3. Install python3: `brew install python3`


### Install pipenv

We'll be using `pipenv` to create a virtual build environment. If you're not familiar with `pipenv`, it combines pip package management along with a virtual environment into a simple Pipfile, which is included in this repo. To install `pipenv` (and upgrade pip), run this:

`pip3 install --upgrade pip pipenv`

### Set up your environment

Now that `pipenv` is installed, we can add in the packages necessary to run your own local docsdev. `cd` into the docsdev folder created by your `git clone` command and run:

`pipenv install mkdocs`

Congratulations! You're all set up!

## Run Masking Docsdev

To run your own local documentation development environment, make sure you're in the docsdev folder and type:

`pipenv run mkdocs serve`

This will run a local `mkdocs` instance on your machine that serves up the documentation at http://localhost:8000/

From here you can make any changes you want to the .md (markdown) files inside docsdev/docs, and the `mkdocs` server will update with your changes on the fly. Easy, good old fashioned editing. 

## ADVANCED: Tinkering with mkdocs

If you really want to get in and do any custom mkdocs development, you can enter a virtualenv shell rather than running mkdocs through the `pipenv run` command. Just run:

`pipenv shell`

This will activate the virtualenv in which you can run `mkdocs serve` or whatever else you want. You can deactivate/exit the shell with the `exit` command or CTRL+D.

## Quick Steps

1. `git clone git@gitlab.delphix.com:docs/docsdev.git && cd docsdev`
2. `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
3. `brew update && brew install python3`
4. `pip3 install --upgrade pip pipenv`
5. `pipenv install`
6. `pipenv run mkdocs serve`

## Running mkdocs after install

When you need to start your local mkdocs server, it's really simple. Just make sure you're in the 'docsdev' directory locally (e.g. `cd ~/docsdev`), then run: `pipenv run mkdocs serve`

## Validation

After preparing your changes and reviewing the rendered HTML in a web browser, you should check to make sure that the documentation does not have any broken links. To do this:

1. Download the latest linkcheck utility from [https://github.com/filiph/linkcheck]()
2. Rename the binary `linkcheck` and install it on your path
3. Assuming you have started a web server on localhost as described above, run the following command `linkcheck --skip-file /path/to/docsdev/linkcheck-skip.txt :8000`
4. Review the output for 404 errors

## Checking in Changes

After following the steps above, you will be ready to make changes to the documentation. Like most other repositories, each change to the documentation is tracked by a JIRA issue. Start by creating a JIRA issue in the DOC project. Next create a branch to work on, use your favorite editor to make changes, view the changes for correctness, and commit the changes using the JIRA issues summary.

Checking in a change requires two ship its on Review Board. The review should include the following groups: all-masking-gate, docs, gatekeepers-docs, masking. There are two ways to post a documentation review:

* `git review`: the familiar command used to post reviews for any Delphix Git repositories

* `git docsdev-review`: a command built specifically for this docsdev repository. The `git docsdev-review` command builds the documentation, copies the documentation to a user specified virtual machine that is running an HTTP server, and then posts a review with a web link to the virtual machine's documentation. The web link is very helpful for reviewers, especially for large reviews or reviews with inline images. For convience, pre-created VM images for use with `git docsdev-review` are available using the docsdev-server group at:
  * Dcenter (`dcenter.delphix.com`)
  * DCoA (`dlpxdc.co`)
See `git docsdev-review -h` for help.
