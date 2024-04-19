# Elixir

## Pattern Matching
In MG, we use pattern matching because it's explicit and really a strong point of using elixir. With that said, we prefer the following:
- Pattern matching over control statements (eg: if-else conditional).
- We write pattern matching rules that cover all scenarios.
- Use guard clauses for complex pattern matching rules.

## Pipe operator
As code gets longer, it becomes harder to read. One of our ways for a clean code is we prefer to only pipe functions when chaining 2 functions or more.

```elixir
# Avoid:
Account
|> function_a()

# Good:
Account
|> function_a()
|> function_b()

  function_a(Account)
```

## Scheduled Jobs

### GenServer
- We use GenServer for resource hungry operations that require asynchronous processing.
- We prefer to use Genserver over Agent.

## Real-Time Features

### LiveView
- With basic understanding of Phoenix channels and Websockets, one should know how LiveView is working underneath.
- Why do we prefer LiveView over reactjs component and when to use full/partial LiveView component

## Graphql and Absinthe
Absinthe is the GraphQL toolkit for Elixir, an implementation of the GraphQL server.
- Present why we use Absinthe and its importance when dealing with GraphQL in elixir.
- Show alternative way like Hasura GraphQL
- Cites examples and limitations of hasura. Case point why we still need absinthe for niche sql queries.
- Point them in our playbook for setup and suggested formats. https://www.mashupgarage.com/playbook/elixir/absinthe.html

