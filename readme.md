# Welcome to the New Face of Delphix Masking Documentation

Delphix Masking is embarking on a great-- nay, a noble quest. It is a quest to break the shackles of Confluence once and for all, and usher in an era of prosperity and great documentation... with Markdown.

## Installation

### Clone this repo

Open your terminal, ```cd``` to whatever top level directory you want and paste:

`git clone git@gitlab.delphix.com:docs/docsdev.git`

Now we need to get Python 3 installed. If you already have it installed, you can skip ahead to **"Install pipenv"**. If you are a savvy adventurer in Pythonland and already have `pipenv` installed, skip to **"Set up your environment"**.

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

`pipenv install`

Congratulations! You're all set up!

## Run Masking Docsdev

To run your own local documentation development environment, make sure you're in the docsdev folder and type:

`pipenv run mkdocs serve`

This will run a local `mkdocs` instance on your machine that serves up the documentation at http://localhost:8000/

From here you can make any changes you want to the .md (markdown) files inside docsdev/docs, and the `mkdocs` server will update with your changes on the fly. Easy, good old fashioned editing. 
