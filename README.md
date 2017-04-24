## Docker-Phoenix image

# Purpose
The image should be used as a base one for building your Phoenix app's image/container

# What's inside
| App | Version |
|----|-------|
| Elixir | 1.4.2 |
| Erlang | 19.3 erts-8.3.1 |
| Hex | 0.16.0 |
| Rebar | 2.6.4 |
| Nodejs | 7.9.0 |
| NPM | 4.5.0 |

# Example usage

```
FROM chvanikoff/phoenix
# Copy our project files to the image
COPY . /var/app/myapp
WORKDIR /var/app/myapp
# Set appropriate MIX_ENV
ENV MIX_ENV prod
# Install node dependencies and compile assets
RUN cd assets \
  && npm install \
  && node_modules/.bin/webpack --progress --colors
# Setup database, compile app and generate digest
RUN mix do ecto.setup, compile, phx.digest
# Run the app with iex shell open
CMD ["iex", "-S", "mix", "phx.server"]
```


