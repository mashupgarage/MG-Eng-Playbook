# Phoenix Docker Setup

Dockerizing a phoenix application can help simplify running and managing projects in your teams. With a docker setup we won't need to install elixir, erlang, postgres, and other dependencies on machines manually and can have consistent behavior between different environments. Here is our recipe for creating a basic phoenix application with docker. This guide assumes that a phoenix application has already been set up using `mix phx.new` or any other method.

## Dockerfile

The Dockerfile gives instructions on how to build a docker image. We usually put commands here for installation, file initialization or directory management. We add it to the root directory of our project with Dockerfile as the filename.

```dockerfile
# replace * with actual elixir version (e.g. elixir:1.14.0)
FROM elixir:*.*.*

RUN mix local.hex --force && mix local.rebar --force

RUN apt-get update \
 && apt-get install -y \
    curl \
    make \
    build-essential \
    sudo \
 && rm -rf /var/lib/apt/lists/*

# replace * with actual node version (e.g. setup_18.x)
RUN curl -sL https://deb.nodesource.com/setup_*.x \
    | bash - && sudo apt-get install -y nodejs

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
	&& echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update -y \
    && apt-get install -y yarn

RUN apt-get install -y inotify-tools

RUN mkdir -p /app
WORKDIR /app
```

For our image we base it off an existing elixir image (e.g. elixir:1.14.0). We can then install dependencies needed for package management which are hex and rebar (needed for erlang). We also should install os dependencies needed to get things to work along with node and yarn. Lastly we can install inotify-tools which is used for live reloading.
