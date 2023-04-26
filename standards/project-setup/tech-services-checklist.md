# Tech Services Checklist

In order to bootstrap a new project effectively, there are some tech services we consider setting up. This is a checklist of things to set up and our recommendations of what to use.

## Code Repository

Each project should have its own repository to track the changes and updates done on the codebase. This repository is also used to facilitate code reviews. For this job we recommend `Github`.

## Continuous integration & development

To continuously test updates to the codebase, we recommend setting up a CI environment that will automatically run all tests and checks as well as deploy automatically. For this we use `SemaphoreCI`.

## Staging Server

To preview and test out updates before deploying to production, we recommend having a staging environment. Developers and QA specialists can use this environment to check if everything is working as intended then ship to production once approved. We recommend `Gigalixir` to set this up. Our previous projects have used `Heroku` but it is no longer recommended. If the project is mostly a front-end project, we recommend `Netlify` or `Vercel`.
