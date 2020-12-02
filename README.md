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
    - You should be able to see three dots in the top right corner. When you do, click on them.
    - Create a new webhook with a conventional name then you should see a URL to copy.
    - Once you have copied the URL from Teams, paste it in the URL box in Jenkins and type the name you gave to the connector.
5. **Source Code Management:**
    - Select `Git`
    - In you repo on GitHub, click on `Code` and then `SSH`. After this, copy the URL and paste it in the `Repository URL` section in Jenkins.
    - SSH Keys with Jenkins and GitHub
        - Navigate to the directory where you can find your SSH keys. `cd ~/.ssh`
        - Generate a new SSH key. `ssh-keygen -t ed25519`
        - When prompted, enter the file name to save the new key into.
        - On GitHub, go to Settings --> SSH and GPG keys --> New SSH Key. This is in order to add the private key (file without .pub extension)
        - Add the public key (filel with .pub extension) to Jenkins by clicking `Add`
        - Specify the branch to build with (*/dev) in the `Branches to build` section.
6. **Build Triggers:**
    - Tick `GitHub hook trigger for GITScm polling` to make jenkins build automatically everytime you push some changes to GitHun.
7. **Build Environment**
    - Tick the box where it says `Provide Node & npm bin/folder to PATH
8. **Build:**
    - Add a build step with the `Execute shell` option
    - Inside it you want to put in the following commands:
        - `cd App_Multi_Virtual_Machine/app`
        - `npm install`
        - `npm test`
9. Finally `save`
10. Now Jenkins will automatically build and test your code once you push to your specified branch.

## Second Job
Now that the code has been tested, the next step is to make Jenkins automatically merge the `*/dev` branch into the `*/main` branch and push to github.

1. Create another job on Jenkins by clicking `New Item` on the Dashboard.
2. Name the job and select `Freestyle Project`.
3. **General:**
    - Give the job a logical description.
    - Tick the `Discard old builds` box and set the `Max number of builds to keep` at 2 (Helps Jenkins with capacity)
    - Tick `GithHub project` and paste the URL of the repo that you are using.
4. **Office 365 Connector:**
    - Paste the notification webhook by going into the specific channel in Microsoft Teams.
    - You should be able to see three dots in the top right corner. When you do, click on them.
    - Create a new webhook with a conventional name then you should see a URL to copy.
    - Once you have copied the URL from Teams, paste it in the URL box in Jenkins and type the name you gave to the connector.
5. **Source Code Management:**
    - Select `Git`
    - In you repo on GitHub, click on `Code` and then `SSH`. After this, copy the URL and paste it in the `Repository URL` section in Jenkins.
    - Select the public key that was created in the first job.
    - Specify which brand you want to build
    - Go to `Additional Behaviours` and select `Merge before build`
    - Set the `Name of repository` to `origin`.
    - Set the `Branch to merge to` section to `main` or `master` depending on what you have named it.
6. **Build Triggers:**
    - Tick the `Build after other projects are built` so that Jenkins can merge and push everytime a build is successful.
    - In the `Projects to watch` section, enter the name of your first job.
    - Tick `Trigger only if build is stable`
7. **Post-build Actions:**
    - Click the dropdown menue, `Add post-build section` and select `Git Publisher`
    - Tick `Push only if the build succeeds`
    - Tick `Merge Results`
8. Finally save this