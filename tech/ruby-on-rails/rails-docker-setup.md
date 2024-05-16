# Rails Docker Setup

Dockerizing a rails application can help simplify running and managing projects in your teams. With a docker setup we won't need to install rails, postgres, and other dependencies on machines manually and can have consistent behavior between different environments. Here is our recipe for creating a basic rails application with docker. This guide assumes that a rails application has already been set up using `rails new` or any other method.

## Dockerfile

The Dockerfile gives instructions on how to build a docker image. We usually put commands here for installation, file initialization or directory management.

```dockerfile
# replace * with actual ruby version e.g. ruby:3.1.2
FROM ruby:*.*.*

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev libyaml-dev

# Node.js. Replace * with actual version to use e.g. setup_18.x
RUN curl -sL *https://deb.nodesource.com/setup_*.x | bash - \
    && apt-get install -y nodejs

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -\
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn

RUN mkdir /app
WORKDIR /app
```

We first declare the ruby version we'll be using. Then we install dependencies needed for the linux environment. Usually `build-essential` and `libpq-dev` are all we need but in recent experience we usually also need `libyaml-dev` for things to work properly. Then if project needs any form of JS we install node and yarn.
