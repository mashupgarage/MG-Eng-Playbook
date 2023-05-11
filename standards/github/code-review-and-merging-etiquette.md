# Code Review and Merging Etiquette

Aside from creating effective pull requests, it's also important to communicate these changes to the team in a timely manner. This would enable issues to be found and addressed as early as possible and prevent wasting time and effort. Here is the etiquette we practice and recommend for conducting code reviews.

## Notify Reviewers ASAP

Reviewers might not always have the time to check for updates in the codebase. To make these changes visible we recommend to notify the relevant people as soon as it's ready. The work doesn't even need to be fully complete yet and can be a work in progress that you just want feedback on. The simplest way to do this is to send a message on slack (or any communication tool) with a link to the PR and the necessary details and screenshots so that they can understand it easily. These are some examples:
	- ✅ Hey everyone I need some reviews on this PR. Our target is to release this today if everything goes well.
	- ✅ I want to hear everyone's thoughts on including the following rules to our linter. I've done a basic config in this PR and will test it out further if you guys agree.
	- ✅ This is my progress so far on implementing the comments section. I would appreciate some feedback especially on the queries I used.
	- ✅ I've been able to fix the invoice report so far but I'm a bit confused if this behavior is what we want. Can you have a look?

## Require approvals before merging

We recommend at least 1 approval before merging work into the main branches. We can enforce this using github's branch protection options.
