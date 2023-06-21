# Stand Up/Stand Down Guide

A stand up meeting (shortened to stand up) is a communication tool used to keep the team up to date with what's happening in a project. Usually it is held as an online meeting but most projects go for an asynchronous version that uses a form submission instead. It's important to fill this up daily to maintain good visibility to team mates, project managers and clients. To make it most effective, here are some guidelines we follow along with examples:

## Categorize your tasks

As much as possible, make sure to list down everything work related you did for the day. These can fall into categories like the following:

### TICKET
Anything directly related to working on tickets including development, pairing, and testing. You can use the ticket name or describe the task. It also helps to put a url that links directly to the ticket.
- ✅ (TICKET) Started working on admin sees new dashboard design (example.com/ticket-001)
- ✅ (TICKET) Done with admin sees read receipts for emails (example.com/ticket-002)
- ✅ (TICKET) (WIP) Investigate missing invoices (example.com/ticket-003)
- ✅ (TICKET) Done with User Account Improvements part 1 (example.com/ticket-004)

### RELEASE
Anything related to releases such as reviews and management.
- ✅ (RELEASE) Managed release 1.2.1
- ✅ (RELEASE) Reviewed PRs for upcoming releases

### MEETING
Any meetings attended for the day
- ✅ (MEETING) MG Engineering Team
- ✅ (MEETING) CPR Discussion

### STUDY
Time spent learning new things that may or may not be related to current tickets
- ✅ (STUDY) Changes in new Elixir version
- ✅ (STUDY) How to use hooks in react

### OTHER
Anything else work related that are not directly related to tickets like attending events, investigating issues, or chores
- ✅ (OTHER) Attended code cuts
- ✅ (OTHER) Hosted CSS blitz
- ✅ (OTHER) Investigated bug related to 2FA on staging
- ✅ (OTHER) Wrote guides on react forms

## Indicate progress of tasks

When tasks span more than a day or are done in installments add some states that give indication of the progress of your tasks. A task can be in one of the following states:

### Started
The task does not have any significant progress yet.
- ✅ (TICKET) Started working on Admin sees updated risk codes (example.com/ticket-005)
- ✅ (OTHER) Started writing a guide on 2FA in dev wiki
### Work in Progress (WIP)
The task has significant progress but there are still some stuff to do.
- ✅ (TICKET) (WIP) Working on Admin can archive posts (example.com/ticket-006)
- ✅ (STUDY) (WIP) Reading on best practices for writing ruby services
### Done
The task has been completed. For tickets, they should be counted as done once the PR has enough approvals (will vary based on project approval process).
- ✅ (TICKET) Done with design for updated admin nav bar (example.com/ticket-007)
- ✅ (OTHER) Completed first draft of github guide

## Indicate subtasks

Sometimes the task description doesn't give the whole idea of what happened but would be too long if we put everything in that description. In these cases it's useful to list down the specific subtasks under that task. Some examples:
- ✅ (TICKET) Started working on admin sees new dashboard design (example.com/ticket-001)
    - Organized css of page
    - Consulted designer on some sections
- ✅ (TICKET) (WIP) investigate missing invoices (example.com/ticket-003)
    - Paired with Ady to address bug with invoice API
- ✅ (TICKET) Done with Drawdown Improvements (example.com/ticket-004)
    - Helped test drawdown improvements on staging
- ✅ (OTHER) (WIP) Update webpack setup
    - Updated typescript version
    - Reconfigured breaking changes on new webpack version

## Communicate blockers or issues encountered

A blocker is anything that has a significant effect on the time taken to do a ticket. If it’s something that makes you go beyond initial estimate then it’s a blocker. We should communicate these openly so that we know why a ticket went beyond its initial estimate and to know if any devs need help to get unblocked. Some examples:

### Waiting for something from client side
- Waiting for confirmation from admin team regarding repayment adjustments
- Still following up client on credentials we need for Algolia search integration
- There are some details regarding invoice approval that aren’t clear

### Unexpected learning curve for something related to card (beyond initial learning curve estimate)
- The Salesforce API had an update and some syntax changed
- I had to study the pagination gem closely because it had a issue with dealing with filtered data
- Devise gem had a special implementation that I had to study in more depth
- The task needed to use a reducer which I’m unfamiliar with

### Dealing with some issues with previous (or current) implementation
- I had to refactor the existing code because it was not flexible to deal with new filter
- Previous API was bugged and I had to do a workaround

### Unforeseen additional tasks to do in ticket (sometimes solution is just to make new ticket)
- There was a change in the design which wasn’t suitable for current implementation
- There was a last minute change of formula for the computations that changes how data is displayed in the page
- The Twilio API was down for most of the day

### External Factors
- There was a power interruption which delayed progress on tasks
- Machine frequently slowed down because of a docker issue
