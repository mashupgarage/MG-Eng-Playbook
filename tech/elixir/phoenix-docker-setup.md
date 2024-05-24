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

## Docker compose

When running applications in docker, we generally prefer to break things down into services and docker compose is the tool we use to achieve this. At minimum, we recommend to split the application into a web service and a db service. We declare our services in a `docker-compose.yml` file, which we put in the root directory of our project:

```yaml
version: '3'

services:
  web:
    build: .
    volumes:
      - '.:/app'
      - 'node_modules:/app/node_modules'
      - 'assets_node_modules:/app/assets/node_modules'
      - 'build:/app/_build'
    ports:
      - '4000:4000'
    depends_on:
      - db
    stdin_open: true
    tty: true
    command: 'mix phx.server'
    environment:
      - DATABASE_URL=${DATABASE_URL}

  db:
    image: postgres:15
    volumes:
      - 'pgdata:/var/lib/postgresql/data'
    ports:
      - '5432:5432'
    environment:
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}

volumes:
  pgdata:
  node_modules:
  assets_node_modules:
  build:
```

The `web` service is our main service that we'll use to start our phoenix application. We specify `build .` to make it use the image we built in the `Dockerfile` in the same directory. To persist some of our dependencies on the host machine we use volumes for `node_modules` (Node.js modules), `assets_node_modules` (Node.js modules for phoenix projects), and `build` (elixir build files) so we don't need to install every time. We specify port 4000 so that when the service runs the specified command it will use that port. This can be changed to any port applicable and available. Lastly for any environment variables needed we store them in a `.env` file in the root of the project.

The `db` service uses a prebuilt postgres image and persists its data using a volume. We usually use port 5432 but this can be anything depending on port availability. We also use a `.env` file to store needed information like the password.