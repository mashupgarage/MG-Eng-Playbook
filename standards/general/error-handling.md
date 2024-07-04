# Error Handling

An application with zero bugs does not exist. No matter how well written code is, runtime errors and unexpected behavior can still happen at some point. Hence, the most we can do is be prepared to handle these issues such that they don't bring down the application and can be addressed ASAP. These are some principles we follow to handle errors effectively.

## Keep errors visible

As mentioned above, the chances of an error happening will never be zero and when they happen it should be clear that there is an issue. The more visible an error is, the faster it can be debugged and addressed. As such it's important to handle errors gracefully and provide proper messages or log them. For cases where certain errors can't be ignored because they can cause unusual behavior or prevent proper flow (e.g. disconnections, deleting something that doesn't exist, invalid dependent data) it's recommended to throw/raise exceptions so we can easily see where and why an error happened.

## Use specific error messages

The most common practice for handling errors is to display a message such as `Something went wrong` or `There is an error`. These messages are too generic though and while they may work initially they may become less useful for finding out what went wrong. This can become more of an issue as a codebase grows. If all error cases provide the same generic message it can be more difficult to narrow down what the issue is. When working with familiar code maybe it won't be much of an issue but when other developers with less familiarity step in (which more often than not happens) they may struggle to trace the issues.

To address this problem, we should tailor error messages to specific scenarios like `There was a network error` for connection errors or `Failed to create post` for post related errors. The amount of specificity in detail will depend on the specifications of the feature or team conventions. As a project scales, it may also help to introduce error codes or custom error objects to record needed details.

## Catch specific exceptions

For critical errors that can affect program correctness, we call these exceptions, it's a common practice to catch/handle them to prevent the application from crashing. Similar to point above on error messages, we should make these as specific as possible to be able to narrow down what went wrong. Most programming languages provide mechanisms to specify what exceptions to respond to and some even provide ways to create custom exceptions for specific use cases.

## Provide proper logging

As applications grow in complexity, it may not be enough to just look at error messages at the moment of the error. We need a system to persist or log the steps taken by the application to get a clearer idea of what happened. Most technologies have built in tools such as stack traces but in some cases it may help to use bug tracking tools such as `Bugsnag`.
