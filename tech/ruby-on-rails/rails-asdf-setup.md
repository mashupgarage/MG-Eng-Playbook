# Install ruby on rails using ASDF
This topic tackles on ruby on rails installation thru <a href="https://asdf-vm.com/guide/introduction.html" target="_blank">asdf</a> version manager.

## Prerequisites

- Asdf tool version manager
- Build essentials
- Ruby
- Nodejs
- Yarn (optional)

## Asdf setup

Please refer to <a href="/tools/asdf.md">this page</a> for the installation setup for asdf.

## Installing build essentials
These apps are the recommended tools to install in your machine so you won't get any dependency issues during setup and/or development.

1. Installing all dependencies
```
# In ubuntu run the following commands:
sudo apt-get update
sudo apt-get install openssl -y
sudo apt-get install build-essential
sudo apt-get install libz-dev
sudo apt-get install libyaml-dev
sudo apt-get install libssl-dev -y
```
> In arch linux you can run `sudo pacman -S base-devel` instead of build-essential.

> Windows WSL typically installs ubuntu so the command above can be used under WSL2.

## Installing ruby on rails

1. Installing latest ruby thru asdf
```
asdf plugin add ruby https://github.com/asdf-vm/asdf-ruby.git
asdf install ruby latest
asdf global ruby latest

# see ruby version to check if installation is successful.
ruby -v
```

2. Installing nodejs & yarn
```
asdf plugin add nodejs
asdf plugin add yarn
asdf install nodejs latest
asdf install yarn latest
asdf global yarn latest
asdf global nodejs latest

# check if installation is successful
 yarn -v
```

> All the packages listed above can also be defined in .tool-versions file. You can specify all your plugins and install in 1 go with just `asdf install` command.
3. Installing Postgresql
```
# Install some dependencies
sudo apt-get install build-essential libssl-dev libreadline-dev zlib1g-dev \
libcurl4-openssl-dev uuid-dev icu-devtools libicu-dev

# Install postgresql
asdf plugin-add postgres

# We might have an specific version supported on the server so using latest here is not a good idea.
# Pls refer to your cloud server for the compatible version.
asdf install postgres <version>

# Starting the postgres app
pg_ctl start

```

> To stop the app use `pg_ctl stop` command

4. Installing Rails
```
gem install rails
gem install pg
gem update --system

# check rails installation
rails -v
```

## Rails application up and running

1. Creating new project
```
# using rails new <project_name> command with postgresql as the database
rails new blog -d postgresql
cd blog
gem install bundler
bundle install
```

2. Initialize the server
```
rails s
```

That’s all folks! You now have your rails application up and running. For more info about rails, you can check the documentation <a href="https://guides.rubyonrails.org/v5.0/getting_started.html"> here </a>