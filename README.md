# Docs

Repository with docs for our API service

## Setup

This repository uses [MkDocs][1] with [Material][2] theme. We use [Docker][3]
for development.

## Development

See here for more info on how to develop using their the theme's docker image.
To start a development server:

```sh
$ docker compose up
```

Your server will be available on `localhost:8000`.

## Quirks

Please, use the docker compose configuration to start you container. It avoids
some weird problems with file permissions and such.

[1]: https://www.mkdocs.org/
[2]: https://squidfunk.github.io/mkdocs-material/
[3]: https://www.docker.com/
