# Elixir Competencies

## Functional Programming

### Description
Developers should have a solid understanding of functional programming concepts such as immutability, recursion, higher-order functions, pattern matching, and immutable data structures.

## Examples

- Able to use pattern match effectively.
- Understands how immutable and mutable data works.
- Able to loop using recursion and high level functions.


## Syntax and Core library Familiarity

### Description

Developers should be comfortable with Elixir syntax, data types (atoms, tuples, lists, maps), modules, functions, and core libraries. Understanding how to leverage built-in functions and modules effectively is essential for writing idiomatic Elixir code.

## Examples

- Able to define public and private methods
  ```elixir
  def sameple, do: true
  defp private, do: true
  ```
- Able to use pattern match effectively.
  ```elixir
  def fetch_name(%{name: nil}), do: "no name found"
  def fetch_name(%{name: person_name}), do: person_name
  # catch any matching case
  def fetch_name(_data), do: "invalid data"

  ```
- Knows built in function and its usage such as Enum and String function.

## Concurrent Programming

### Description
Elixir leverages the Erlang Virtual Machine (BEAM), which excels at concurrency and distribution. Developers should be proficient in working with concurrent processes (OTP, supervisors etc).

### Examples

- Be able to setup a concurrent module that utilizes the built-in functions like spawn, send and receive.
```elixir
defmodule ConcurrentExample do
  def start do
    # Start two processes
    pid1 = spawn_link(__MODULE__, :process_one, [])
    pid2 = spawn_link(__MODULE__, :process_two, [])

    # Send messages to the processes
    send(pid1, {:hello, self()})
    send(pid2, {:world, self()})

    # Wait for responses
    receive do
      msg ->
        IO.puts("Received message from Process 1: #{inspect(msg)}")
    end

    receive do
      msg ->
        IO.puts("Received message from Process 2: #{inspect(msg)}")
    end
  end

  def process_one do
    receive do
      {:hello, sender} ->
        send(sender, "Hello from Process 1")
    end
  end

  def process_two do
    receive do
      {:world, sender} ->
        send(sender, "World from Process 2")
    end
  end
end

ConcurrentExample.start()

```

## Elixir tooling

### Description
Elixir specially the Phoenix framework comes with varierty of tools including the Mix build tool, Hex package manager, and IEx interactive shell. Understand the usage of these tools is crucial for effective development.

### Examples

- Understands how build tools are used.
- Manage libraries with hex package manager.
- Be able to interact with IEx shell.

## Ecto and Database Interactions

### Description
Ecto is the database library for Elixir, providing a powerful query interface and schema abstraction. Developers should be proficient in defining schemas, writing queries, performing CRUD operations, and managing database migrations using Ecto.

### Examples

- Be able to interpret queries using Ecto.
```elixir
# sample sql
Select * from users where age > 18;

# Ecto
Repo.all(from u in "users",
          where: u.age > 18)
```
- Can define schemas.
- Manage database migrations.

## MVC framework

### Description
Developers should be skilled in building web applications with Phoenix, structuring applications using MVC architecture, handling HTTP requests, and implementing server-side and client-side logic.

### Examples

- Understanding on how model-view-controller works.
- Be able to develop an app using the said architecture.

## Testing

### Description
Developers should be adept at writing unit tests, integration tests, and end-to-end tests. These can be done using the built-in ExUnit testing framework in Phoenix.

### Examples

- Able to write unit tests
```elixir
test "get_all_users retrieves all users" do
  users = User.get_all_users()
  assert length(users) == 2
  # Add more assertions based on your test data
end
```