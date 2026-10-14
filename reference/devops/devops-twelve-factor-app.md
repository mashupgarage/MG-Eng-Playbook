# 12 Factor App
A basic illustration of the big picture when it comes to DevOps engineering.

## Codebase
A single code repository for an application
Concept is akin to a central hub for code collaboration
Example would be Git, Gitlab, Github, Bitbucket
Applications serving different services should live on a separate repo

Each application should have a server setup such as:
  * Development
  * Staging
  * Production

## Dependencies
Declare and isolate dependencies due to the fact that dependencies differ for each application
A list of dependencies for modern programming languages are represented on manifest type files:
  * Gemfile for Ruby on Rails apps
  * mix.exs for Elixir Phoenix apps
  * requirements.txt for Python

Managing virtual environments, ensures application has its own dependencies to themselves
  * And also, for OS dependencies, the same could be said about managing virtual environments as a solution.
  * Think of containerization (Docker is the platform of choice)

## Concurrency
Is a set of strategies on how we adapt to the ever changing demand for application service availability.
We do that by introducing scaling strategies.

### Vertical Scaling
Is to scale server capability by adding hardware resources to your currently running machines.
Downside is we introduce downtime when updating resources.

### Horizontal Scaling
Is to scale server capability by adding in additional nodes (new instances of an application) managed by
a load balancer

## Processes access to resources
Characterized by processes such as getting user information, display user information, session record etc.
It should be residing on one single place, like a single source of truth for all information.
Example of this are:
* Redis
* Databases
* File hosting (S3)

## Backing Services/Config
Ability to point resources easily without much change in code
Examples are env variables for url configuration, port configurations etc.
