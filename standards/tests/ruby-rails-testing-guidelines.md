# Ruby/Rails Testing Guidelines

When testing code written in Ruby on Rails, there are some scenarios or points of confusion that we encounter from time to time. Here are some guidelines we follow to make testing more effective.

## Avoid controller testing pitfalls

Controller specs tend to be slow because they deal with rendering full pages and when overused can result in a slow running CI. Aside from that controller specs may overlap with end-to-end testing (also called feature specs) which is usually handled with different tools (e.g. Ghost Inspector, Cypress). Use controller specs in the following scenarios:
- ✅ routing (e.g. does it redirect, can a certain user access the page )
- ❌ conditional rendering of elements on the page like buttons (more for end-to-end testing)
- ❌ controller action logic (if your actions have complex logic better to extract to a service and test that)
