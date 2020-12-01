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
1. Clone this repo
2. Run `vagrant up`
3. Go to `development.local:3000` or `192.168.10.100:3000`
4. 
### Getting set up/ Pre Requisits
* set up vagrant
* ruby
* Vagrant

### Running the Environment
### Running the tests