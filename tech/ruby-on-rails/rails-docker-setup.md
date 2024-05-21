# Rails Docker Setup

Dockerizing a rails application can help simplify running and managing projects in your teams. With a docker setup we won't need to install rails, postgres, and other dependencies on machines manually and can have consistent behavior between different environments. Here is our recipe for creating a basic rails application with docker. This guide assumes that a rails application has already been set up using `rails new` or any other method.

## Dockerfile

The Dockerfile gives instructions on how to build a docker image. We usually put commands here for installation, file initialization or directory management. We add it to the root directory of our project with `Dockerfile` as the filename.

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

## Docker compose

When running applications in docker, we generally prefer to break things down into services and docker compose is the tool we use to achieve this. At minimum, we recommend to split the application into a web service and a db service. We declare our services in a `docker-compose.yml` file, which we put in the root directory of our project:

```yaml
version: '3'

services:
  web:
    build: .
    command: /bin/sh -c "rm -f /app/tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    volumes:
      - '.:/app'
      - 'rubygems:/usr/local/bundle'
      - 'node_modules:/app/node_modules'
    ports:
      - '3000:3000'
    depends_on:
      - db

  db:
    image: postgres:15
    volumes:
      - 'pgdata:/var/lib/postgresql/data'
    ports:
      - '5432'
    environment:
      POSTGRES_PASSWORD: postgres
      PGPASSWORD: postgres

volumes:
  rubygems:
  pgdata:
  node_modules:
```

The `web` service is our main service that we'll use to start our rails application. We specify `build: .` to make it use the image we built with the `Dockerfile` in the same directory. When the project is up this service will run a rails server on port 3000. To persist some of our dependencies on the host machine we can also create some volumes for our gems (bundle) and node modules so they don't need to install every time. Lastly we add a dependency to the db service which we will discuss next.

The `db` service uses a prebuilt postgres image and persists its data using a volume. We usually use port 5432 but this can be anything depending on port availability. We then specify the postgres password for authentication when accessing the db.

These two services are usually enough to get a project up and running then other services can be added as needed. For example if we run `webpack` for js bundling we can also create a service for that. If the project needs background jobs we can also set up services for `redis` and `sidekiq`.
