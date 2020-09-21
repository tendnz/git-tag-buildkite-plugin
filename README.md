# Git Tag Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) to tag the current head with a version and push it to the repo.

Based heavily on [Git Commit](https://github.com/thedyrt/git-commit-buildkite-plugin).

## Example

With no options, tags the `$BUILDKITE_BRANCH` and pushes the tags, with a commit message like `Build #4`:

```yml
steps:
  - command: make
    plugins:
      - tendnz/git-tag#v1.0.0:
          version: "v1.0.0-prod" 
```

With all options customized:

```yml
steps:
  - command: make
    plugins:
      - tendnz/git-tag#v1.0.0:
          version: "v1.0.0-prod"
          message: "Release to $ENV [$BUILDKITE_BUILD_NUMBER]"
          user:
            name: Bob Monkey
            email: bob@codemonkeys.com
```

## Configuration

- **version** (required))

    A tag to use in `git tag $VERSION`

- **message** (optional, defaults to `Build #${BUILDKITE_BUILD_NUMBER}`)

    The commit message

- **user.email** (optional)

    If given, will configure the git user email for the repo.

- **user.name** (optional)

    If given, will configure the git user name for the repo.


## Tests / Linting

To run the tests of this plugin, run

```sh
docker-compose run --rm tests
```

To run the [Buildkite Plugin Linter](https://github.com/buildkite-plugins/buildkite-plugin-linter), run

```sh
docker-compose run --rm lint
```

## License

MIT (see [LICENSE](LICENSE))
