# Github Actions (Overview)

Is a CI/CD platform that allows you to automate your build, test and deployment pipelines.
You can configure GA to trigger on every push, creation of a PR and or whenever a PR is merged(main, master or what not).

Sits right under the **build stage** of the devops cycle
GA allows you to run **workflows** when other **events** happen in your repository.
For these **workflows** to run, GA provides Linux, Windows and MacOs virtual machines.

## Components

### Workflows
Is a configurable automated process that can run jobs.
It is of YAML format and checked in along with your repository.
Sits under the `.github/workflows` directory of your codebase

Use cases would be:
* manage build
* manage execution of tests
* manage deployment to a cloud services provider

### Events
Is an activity on the repository that stands as a trigger for workflows to run.

Example events are:
* newly opened pull request
* issues opened
* commits pushed to a repo
* scheduled event

For a comprehensive list of **events**, reference [this](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

### Jobs
Is a set of steps in workflow that is executed on the same runner.
These steps are akin to a shell script or an **action** that will be run.

### Actions
Are in short, are macros that you create to avoid repetition.

Example use cases are:
* setting-up authentication to your cloud provider
* pulling from a git repository
* setup toolchain (installation of npm, yarn etc.)

### Runners
Is a server that runs your workflows.
Take note that each runner can run a single job at a time.
Github provides Ubuntu Linux, Windows and MacOs flavaors for OS.
In short, they are VMs that runs these workflows

### Reference
[Github Actions Quickstart](https://docs.github.com/en/actions/quickstart)

