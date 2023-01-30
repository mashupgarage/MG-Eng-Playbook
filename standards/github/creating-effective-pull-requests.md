# Creating Effective Pull Requests
A Pull Request (PR) is our primary means of communicating code changes in our projects. We encourage developers to do code reviews to check that PRs achieve their goals and are up to standard. As reviewers may be busy or don't always have the full context of the code changes, we want to put as much detail as possible to make reviews faster and easier. Here are some tips to make PRs more effective:

## Keep it Small
- Ideally PRs should be not more than 700 additions/deletions
- If PR grows beyond that consider asking if ticket needs to be split into smaller ones
- If a big PR for a single feature is unavoidable consider branching out and splitting parts of the feature (e.g. backend, frontend, tests) into smaller PRs

## Provide a Detailed Description
- What did the PR accomplish?
	- ✅ This PR implemented a sorting feature for admin users.
	- ✅ This PR improves the loading time of the dashboard and cleans up the UI a bit.
	- ✅ This PR fixed a bug where some users were unable to log in.
- How did it accomplish that?
	- ✅ I used a JS library for sorting tables in the frontend.
	- ✅ I found out that there were n+1 queries so I updated them. Some CSS rules were also improved to be more reusable.
	- ✅ I had to update the authentication gem to the latest version as mentioned in the documentation.
- Why was it accomplished as such? (if applicable) Are there limitations or special conditions for the approach?
	- ✅ The sorted UI tables only worked for the admin users table because it only displays a small amount of data. This approach is not practical for large and paginated tables.
	- ✅ But I also found out that the components also take long to load into UI. Will improve this in the next PR.
	- ✅ The latest version of the gem also had a security patch but now CI displays warnings of coming deprecation. Users can now log in again but we will need to update our authentication modules to use the new syntax which we can do in the next PRs.
- Sometimes it's better to over communicate than under communicate

## Provide screenshots or screen capture
- Do only if applicable. It might not be needed for backend changes for example
- Add a short description of what happened for each screenshot
- Use a gif when you need to show a series of interactions
- For bugfix tickets, consider putting a before and after section
- Show desktop, tablet, or mobile views when applicable
