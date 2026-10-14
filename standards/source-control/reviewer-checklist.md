# Reviewer Checklist

As a PR reviewer it is your job to double check PRs if they are up to standard and achieve the goals of tickets. Also remember that PR reviews do not have to be limited to those with expertise. Don’t hesitate to review even when you’re not an expert on the area. Ask questions in unfamiliar areas to clarify or find out more about things. Learn from each others’ code.
When reviewing, especially if time is limited, prioritize this order:

## It should work

This is the most important part. If there’s any part here that is not resolved the PR should not be approved or changes need to be requested

- Does it fulfill the goals of the ticket? (read and understand ticket first)
- Are all the specifications of the ticket found in the code? (ask team or client if anything unclear)
- Is the feature not a duplicate of an existing one?
- Did it cover all cases including edge cases?
- Are there relevant tests that check all the cases?
- Are the tests and CI passing?

## It should be efficient

Working code is the minimum requirement but efficiency should also be checked to future proof features. Depending on difficulty these can either be addressed in current PR or in another one

- Did the PR follow best practices?
- Are any external functions used deprecated?
- Are functions/components/styles reusable?
- Is the UI responsive? (only if responsiveness is implemented in project)
- Are there any slow running tests that can be improved?

## It should be readable

Should be last priority because either the linters already prevented these issues or these changes require a bit more time and can be done in next tickets

- Do variable and function names clearly reflect what they do?
- Are any files too long and need to be split?
- Are there any code smells that need to be addressed?
- Are there any parts in the code that took you or colleagues some time to understand?
- Are filenames easy to search?
- Is the PR description complete and meaningful?
- Did the PR follow team conventions?
