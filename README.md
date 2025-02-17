# repo-template-go

[![tests](https://github.com/ianlewis/repo-template-go/actions/workflows/pre-submit.units.yml/badge.svg)](https://github.com/ianlewis/repo-template-go/actions/workflows/pre-submit.units.yml)

Repository template for Go repos under github.com/ianlewis

This repository template is maintained for use in repos under
`github.com/ianlewis`. However, it can be used as a general purpose Go
repository starter template.

## Usage

1. Update `go.mod`

   The `module` directive in `go.mod` must be updated to the correct module
   name. The `go` directive sohuld be updated to the required Go version.

   ```text
   module github.com/user/repo

   go 1.23.2
   ```

## Makefile

The `Makefile` is used for managing files and maintaining code quality. It
includes a default `help` target that prints all make targets and their
descriptions grouped by function.

```shell
Usage: make [COMMAND]

  help                 Shows all targets and help from the Makefile (this message).
Testing
  unit-test            Runs all unit tests.
  go-test              Runs Go unit tests.
Benchmarking
  go-benchmark         Runs Go benchmarks.
Tools
  license-headers      Update license headers.
  format               Format all files
  md-format            Format Markdown files.
  yaml-format          Format YAML files.
  go-format            Format Go files (gofumpt).
Linters
  lint                 Run all linters.
  actionlint           Runs the actionlint linter.
  markdownlint         Runs the markdownlint linter.
  yamllint             Runs the yamllint linter.
  golangci-lint        Runs the golangci-lint linter.
Maintenance
  clean                Delete temporary files.
```

## Formating and linting

Some `Makefile` targets for basic formatters and linters are included along
with GitHub Actions pre-submits. Versioning of these tools is done via the
`requirements.txt` and `packages.json`. This is so that the versions can be
maintained and updated via `dependabot`-like tooling.

Required runtimes:

- [`Go`]: The Go runtime needs to be installed.
- [`Node.js`]: Node.js is required to run some linters and formatters.
- [`Python`]: Node.js is required to run some linters and formatters.

The following tools need to be installed:

- [`actionlint`]: For linting GitHub Actions workflows.
- [`golangci-lint`]: For linting Go code.
- [`shellcheck`]: For linting shell code in GitHub Actions workflows.

The following tools are installed locally:

- [`yamllint`]: For YAML (e.g. GitHub Actions workflows). (installed in Python
  virtualenv `.venv`).
- [`prettier`]: For formatting markdown and yaml (installed in local
  `node_modules`).
- [`markdownlint`]: For linting markdown (installed in local `node_modules`).

`Makefile` targets and linter/formatter config are designed to respect
`.gitignore` and not cross `git` submodules boundaries. However, you will need
to add files using `git add` for new files before they are picked up.

`Makefile` targets for linters will also produce human-readable output by
default, but will produce errors as [GitHub Actions workflow
commands](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions)
so they can be easily interpreted when run in Pull-Request [status
checks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks).

## License headers

The `license-headers` make target will add license headers to files that are
missing it with the Copyright holder set to the current value of `git config
user.name`.

Files are checked for the existence license headers in pre-submits.

## Project documentation

This repository template includes stub documentation. Examples of
`CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and `SECURITY.md` can be found in the
[ianlewis/ianlewis](https://github.com/ianlewis/ianlewis) repository and are
maintained in line with [GitHub recommended community
standards](https://opensource.guide/).

## Security & Dependencies

In general, dependencies for tools and GitHub Actions are pinned to improved
overall project supply-chain security.

External dependencies on GitHub actions are limited to official GitHub-owned
actions to minimize exposure to compromise of external repositories.

## Keeping repositories in sync

You can optionally keep repositories created with the template in sync with
changes to the template. Because repositories created from GitHub templates are
not forks, it is recommended to to a squash merge to squash the merge as a
commit on your commit history.

```shell
# One time step: Add the repository template as a remote.
git remote add repo-template-go git@github.com:ianlewis/repo-template-go.git

# Fetch the latest version of the repo-template-go.
git fetch repo-template-go main

# Create a new squash merge commit.
git merge --no-edit --signoff --squash --allow-unrelated-histories repo-template-go/main
```

## Contributing

See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for contributor documentation.

[`Go`]: https://go.dev/
[`Node.js`]: https://nodejs.org/
[`Python`]: https://www.python.org/
[`actionlint`]: https://github.com/rhysd/actionlint
[`golangci-lint`]: https://github.com/golangci/golangci-lint
[`markdownlint`]: https://github.com/DavidAnson/markdownlint
[`prettier`]: https://prettier.io/
[`shellcheck`]: https://www.shellcheck.net/
[`yamllint`]: https://www.yamllint.com/
