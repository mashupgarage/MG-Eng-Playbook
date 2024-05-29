# Next JS Docker Setup

Dockerizing a Next.js application can help simplify running and managing projects in your teams. With a docker setup we won't need to install node, yarn, and other dependencies on machines manually and can have consistent behavior between different environments. Here is our recipe for creating a basic Next.js application with docker. This guide assumes that an application has already been set up like in our [guide](/tech/nextjs/setting-up-next-js.md) or any other method.

## Dockerfile

The Dockerfile gives instructions on how to build a docker image. We usually put commands here for installation, file initialization or directory management. We add it to the root directory of our project with Dockerfile as the filename.

```dockerfile
# replace * with actual version (e.g. node:18.20.0)
FROM node:*.*.*

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -\
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn

RUN mkdir /app
WORKDIR /app
```

We base off our application image on a prebuilt node js image. Take note that Next.js requires at least node 16 and newer versions recommend 18. We also install yarn as our choice of package manager.
