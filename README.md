# Git Tag Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) to tag the current head with a version and push it to the repo. Also makes a release
in Github if you provide the right details

Based heavily on [Git Commit](https://github.com/thedyrt/git-commit-buildkite-plugin).

## Example

With no options, tags the `$BUILDKITE_BRANCH` and pushes the tags, with a commit message like `Build #4`:

```yml
steps:
  - command: make
    plugins:
      - tendnz/git-tag#v1.0.7:
          version: "v1.0.0-prod" 
```

With all options customized:

```yml
steps:
  - command: make
    plugins:
      - tendnz/git-tag#v1.0.7:
          version: "v1.0.0-prod"
          message: "Release to $ENV [$BUILDKITE_BUILD_NUMBER]"
          githubtoken: $MY_GITHUB_TOKEN
          reponame: tendnz/my-repo-name
          prerelease: true
          user:
            - name: Bob Monkey
            - email: bob@codemonkeys.com
```

## Configuration

- **version** (required))

    A tag to use in `git tag $VERSION`

- **message** (optional, defaults to `$BUILDKITE_ORGANIZATION_SLUG/$BUILDKITE_PIPELINE_SLUG: Build $BUILDKITE_BUILD_NUMBER for $BUILDKITE_BRANCH"`)

    The commit message

- **githubtoken** (optional, required to enable releases)

    If provided, this will attempt to make a release. Load your token into your ENV (as per all secrets) then use 

    ```
      githubtoken: $YOUR_ENV_NAME
    ```

    DONT put it into the YML!

- **reponame** (optional, but required if you want releases)

    The name of the repo, eg tendnz/my-reop-name

- **prerelease** (optional, defaults to `false`)

    Mark this as a prerelease or not.

- **draft** (optional, defaults to `false`)

    Mark this as a draft or not.

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
