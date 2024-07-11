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
sudo apt install openssl -y
sudo apt-get install build-essential
sudo apt-get install libz-dev
sudo apt-get install libyaml-dev
sudo apt-get install libssl-dev -y
```
> In arch linux you can run `sudo pacman -S base-devel` instead of build-essential


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

3. Installing Rails
```
gem install rails
gem update --system

# check rails installation
rails -v
```

## Rails application up and running

1. Creating new project
```
# using rails new <project_name> command
rails new blog
cd blog
gem install bundler
bundle install
```

2. Initialize the server
```
rails s
```

That’s all folks! You now have your rails application up and running. For more info about rails, you can check the documentation <a href="https://guides.rubyonrails.org/v5.0/getting_started.html"> here </a>