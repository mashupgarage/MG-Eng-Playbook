# Phoenix Docker Setup

Dockerizing a phoenix application can help simplify running and managing projects in your teams. With a docker setup we won't need to install elixir, erlang, postgres, and other dependencies on machines manually and can have consistent behavior between different environments. Here is our recipe for creating a basic phoenix application with docker. This guide assumes that a phoenix application has already been set up using `mix phx.new` or any other method.
