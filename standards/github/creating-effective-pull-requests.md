# Creating Effective Pull Requests
A Pull Request (PR) is our primary means of communicating code changes in our projects. We encourage developers to do code reviews to check that PRs achieve their goals and are up to standard. As reviewers may be busy or don't always have the full context of the code changes, we want to put as much detail as possible to make reviews faster and easier. Here are some tips to make PRs more effective:

## Keep it Small
- Ideally PRs should be not more than 700 additions/deletions
- If PR grows beyond that consider asking if ticket needs to be split into smaller ones
- If a big PR for a single feature is unavoidable consider branching out and splitting parts of the feature (e.g. backend, frontend, tests) into smaller PRs

## Provide a Detailed Description
- What did the PR accomplish?
	- ❌ Sorting feature. (Not specific enough)
	- ✅ This PR implemented a sorting feature for admin users in dashboard.
	- ❌ We noticed that the dashboard takes long to load and sometimes times out. Some users have been complaining about this. Find out how we can improve this. (Don't copy the whole ticket text. Summarize the actual measures taken instead.)
	- ✅ This PR improves the loading time of the dashboard and cleans up the styling of the components in the dashboard.
	- ❌ Implemented [Bugfix ticket 1234]() (Actual ticket should be supplemental info not the main content)
	- ❌ https://trello.com/link-to-ticket (Add short description of ticket and not just a link)
	- ✅ This PR fixed a bug where some users were unable to log in ([Bugfix ticket 1234]()).
- How did it accomplish that?
	- ❌ I used a JS library to sort the tables (Which library? Which tables?)
	- ✅ I used the table-sort-js library to sort the admin tables on the frontend side.
	- ✅ I found out that there were n+1 queries when loading the activity feed entries so I updated those queries. Some CSS rules were also improved to be more reusable.
	- ✅ I had to update devise (authentication gem) to the latest version as mentioned in the documentation.
- Why was it accomplished as such? (if applicable) Are there limitations or special conditions for the approach?
	- ✅ The sorting only worked for the admin users table because it only displays a small amount of data. This approach is not practical for large and paginated tables.
	- ✅ But I also found out that the components on the dashboard also take long to load into UI. Will improve this in the next PR.
	- ✅ The latest version of the gem also had a security patch but now CI displays warnings of coming deprecation. Users can now log in again but we will need to update our authentication modules to use the new syntax which we can do in the next PRs.

## Provide screenshots or screen capture
- Do only if applicable. It might not be needed for backend changes for example
- Provide proper descriptions for each item
- Add a short description of what happened for each screenshot
	- ✅ Table displays proper sorting controls
	- ✅ Fixed the excess spacing between the nav bar and content
- Use a gif when you need to show a series of interactions
	- ✅ Table sorts ascending and descending as soon as columns are clicked
	- ✅ Page loads faster after fix
- For bugfix tickets, consider putting a before and after section
	- ✅ Before: User is stuck in login page
	- ✅ After: User is able to login properly
- Show desktop, tablet, or mobile views when applicable
	- ✅ Mobile: Table is compressed but sorting still works as intended
	- ✅ Tablet: Improved size of nav menu in tablet view
