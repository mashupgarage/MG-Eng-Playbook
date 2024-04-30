# Elixir writing standards
Here are out best practices when it comes to Elixir.

## Prefer pattern matching over if-else conditionals

We are heavily inclined on using elixir's pattern matching across our project. This promotes a better readability and organization in the long run. An implementation best suited for a functional oriented app.
```elixir
# Avoid
def hash_password(%{
  changes: { password: password },
  valid?: is_valid
} = changeset) do
  if is_valid do
    # code here
  else 
    # code here
  end
end
```

```
# Good
def hash_password(%{
  changes: { password: password },
  valid?: true
} = changeset) do
  # hash the password and add it to the changeset
end

def hash_password(%{
  changes: { password: _password },
  valid?: false
} = changeset) do
  # add error to changeset because it is not valid
end

def hash_password(changeset), do: changeset
```

## Prefer GenServer over Agents

Avoid using Agents. Use GenServer instead, since Agent is simply a thin wrapper around GenServer.

## Pipe operator
Prefer to only pipe functions when chaining 2 functions or more.

```
# Avoid: this can easily be written without pipnig
some_value
|> some_function()
```

```
# Good
some_value
|> some_function()
|> some_other_function()
```

```
# Also good
some_function(some_value)
```

## Linting
Our preferred code health and formatting checker is <a href="https://github.com/rrrene/credo" target="_blank"  rel="nofollow">Credo</a>, used along with the <a href="https://hexdocs.pm/mix/main/Mix.Tasks.Format.html" target="_blank" rel="nofollow">Built in Format Checker</a>. These are integrated to our CI Pipeline.

```
mix credo --strict
mix format --check-formatted
```

## Concurrent Programming
Leverage Elixir's lightweight processes (actors) and OTP (Open Telecom Platform) for building concurrent and fault-tolerant applications.
```
defmodule ConcurrentExample do
  # Define a worker process
  defmodule Worker do
    def start_link do
      Task.start_link(__MODULE__, :loop, [])
    end

    def loop do
      receive do
        {:square, num, sender} ->
          send(sender, {:square_result, num * num})
          loop()
        :stop ->
          :ok
      end
    end
  end

  # Spawn multiple worker processes
  def start_workers(num_workers) do
    Enum.map(1..num_workers, fn _ ->
      Worker.start_link()
    end)
  end

  # Calculate squares concurrently using worker processes
  def calculate_squares(numbers) do
    workers = start_workers(3)  # Spawn 3 worker processes

    # Send numbers to workers for processing
    Enum.map(numbers, fn num ->
      worker = List.first(workers)
      send(worker, {:square, num, self()})
      worker = List.delete(worker, worker)
      worker
    end)

    # Collect results from workers
    Enum.map(1..length(numbers), fn _ ->
      receive do
        {:square_result, result} ->
          result
      end
    end)
  end
end

# Example usage
numbers = [1, 2, 3, 4, 5]
IO.inspect(ConcurrentExample.calculate_squares(numbers))
```

## Error Handling
Use Elixir's `with` and `try` constructs for error handling, and avoid throwing exceptions for expected errors.

```
# Example using 'with' for error handling
def divide_with_with(a, b) do
  with {:ok, result} <- divide(a, b) do
    result
  else
    {:error, reason} ->
      IO.puts("Error: #{reason}")
      {:error, reason}
  end
end
```
```
# Example using 'try' for error handling
def divide_with_try(a, b) do
  try do
    case divide(a, b) do
      {:ok, result} ->
        result
      {:error, reason} ->
        raise "Error: #{reason}"
    end
  catch
    e -> e
  end
end
```