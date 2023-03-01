# Branch Naming Conventions
As they say, naming is hard. This idea also applies for naming branches. We want branches with names that are easy to understand and straightforward to find. Here are some conventions we use to achieve that:

## Add a category to the branch name
Branches can be grouped based on what they do such as:
- Full features added to the codebase
	- ✅ feature/approve-requests
	- ✅ feature/post-comments
- Fixes to some bugs and issues
	- ✅ fix/invoices-page-error-500
	- ✅ fix/daily-interest-calculations
- Improvements to an existing feature
	- ✅ enhancement/comments-section-css
	- ✅ enhancement/accounts-page-loading-time
- Chores that may or may not be directly related to features
	- ✅ chore/restructure-js-folders
	- ✅ chore/update-to-rails-7
	- ✅ chore/comments-panel-tests

The categories may vary per project but those are the most common ones we would use.

Also there are some exceptions to this convention such as:
- long lived branches
	- ✅ main (or master)
	- ✅ develop
- release branches
	- ✅ rel-1.2.0

## Indicate ticket number in branch name
If using Jira or any platform that has auto generated ticket number, prepend that number to the branch name instead of category. If no ticket just indicate that there is none.
- ✅ matt-123/approve-requests
- ✅ matt-123/approve-requests-tests (in some cases there can be multiple branches for same ticket)
- ✅ no-ticket/upgrade-nodejs-to-18
