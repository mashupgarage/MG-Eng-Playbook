# Setting up docker for Rails application

Here's a simple example of using Docker to run a Rails application:

1. Create a Dockerfile with the following content:

```docker
FROM ruby:latest

RUN apt-get update -qq && apt-get install -y nodejs postgresql-client

WORKDIR /app
COPY Gemfile* ./
RUN bundle install
COPY . .

CMD ["rails", "server", "-b", "0.0.0.0"]
```

2. Build the Docker image:

```docker
docker build -t my_rails_app .
```

3. Run a container with the built image:

```docker
docker run -p 3000:3000 my_rails_app
```

This will run your Rails app on port 3000 and make it accessible at http://localhost:3000.
