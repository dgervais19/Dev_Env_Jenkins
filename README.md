# Sparta NodeJs Sample APP DevEnv and CI

This repo will be a dev env you can copy and set up by running vagrant up.

## Pre Requisits
* Make sure `Virtual Box` is installed.
    - [Install Here](https://www.virtualbox.org/wiki/Downloads) - This allows us to create Virtual Machines (VM)
* Also make sure that `Vagrant`is installed for your specific OS.
    - [Install Here](https://www.vagrantup.com/downloads.html) - This manages our virtual machines in the virtual box.
* Once you have installed `Vagrant` you need to install the `vagrant-hostupdater` plugin
    - `vagrant plugin install vagrant-hostupdater` installs it.
    - `vagrant plugin uninstall vagrant-hostupdater` uninstalls it.

* Another software that needs to be installed is `Ruby`
    - [Install Here](https://www.ruby-lang.org/en/downloads/)
* Once this has finished we need `bundler` to manage the packages for `Ruby`.
    - We can do this by typing `gem install bundler` in the terminal.


**IMPORTANT!**

* You need to have either `serverspec` or `rake` installed for `Ruby`, you will need it
    - If not, go to the `/tests` directory where you will see a `Gemfile`. Within this this directory type `bundle install`.



## Instructions
### Running the app
1. First of all, clone this repo into your machine
2. Go to where your vagrant file is in your newly made directory.
3. Run `vagrant up`
4. Go to `development.local` or `192.168.10.100` in your web browswer to see the app.
### Testing It
1. Navigate to the `/tests` directory.
2. Run `rake spec` to see whether the tests have passed or not.
    - *Remember* - you can use `rake spec:app` or `rake spec:db` in order to test either the app or database on their own.
3. Once this is done, ensure that this is pushed to GitHub.
    - Create a new repository on GitHub.
    - Delete `.git` if necessary with `rm -rf .git` using the terminal.
    - Follow the instructions on your new GitHub repo.

## First Job on Jenkins
1. First we want to go into jenkins and click `New Item`.
2. Name the job and select `Freestyle Project`.
3. **General:**
    - Give the job a logical description.
    - Tick the `Discard old builds` box and set the `Max number of builds to keep` at 2 (Helps Jenkins with capacity)
    - Tick `GithHub project` and paste the URL of the repo that you are using.
4. **Office 365 Connector:**
    - Paste the notification webhook by going into the specific channel in Microsoft Teams.
    

### Running the Environment
### Running the tests