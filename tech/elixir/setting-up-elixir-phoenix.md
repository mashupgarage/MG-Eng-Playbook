# Install elixir phoenix using ASDF

This topic tackles on phoenix framework installation thru <a href="https://asdf-vm.com/guide/introduction.html" target="_blank">asdf</a> version manager.

## Prerequisites

- Asdf tool version manager
- Erlang
- Elixir

## Asdf setup

Please refer to <a href="/tools/asdf.md">this page</a> for the installation setup for asdf.

## Elixir setup thru asdf

1. Add plugins

```
asdf plugin-add erlang <latest or specific version>
asdf plugin-add elixir <latest or specific version>
```

2. Install erlang
```
asdf install erlang <latest or specific version>
asdf global erlang <latest or specific version>
```
> To verify that Erlang is installed correctly, type erl in the terminal, and it should open the Erlang shell.

3. Install elixir
```
asdf install elixir <latest or specific version>
asdf global elixir <latest or specific version>
```
> To verify Elixir is installed, type elixir -v

## Phoenix setup and new project

1. Once we have Elixir and Erlang, we are ready to install the Phoenix application generator. Use the following command in terminal.
```
mix archive.install hex phx_new
```

2. To start a new project, we can run `mix phx.new` from any directory in order to bootstrap our Phoenix application.

Example command to start a project called Hello
```
mix phx.new hello
```
Follow the prompts and install dependencies.

3. If you configure your database in cofig/dev.exs, create and initialize your database using:
```
mix ecto.create
```

4. Start your Phoenix app server with:
```
mix phx.server
```

By default, Phoenix accepts requests on port 4000. If we point our favorite web browser at http://localhost:4000, we should see the Phoenix Framework welcome page.

<h3>Congratulations, your project is now up and running. You can read more about Phoenix framework documentation <a href="https://hexdocs.pm/phoenix/overview.html">here</a> and Elixir <a href="https://elixir-lang.org/docs.html">here</a></h3>