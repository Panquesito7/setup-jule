# Setup Jule <a href="https://jule.dev"><img src="https://raw.githubusercontent.com/julelang/resources/master/jule_icon.svg" height="60px"></a>

[![Action validation](https://github.com/Panquesito7/setup-jule/actions/workflows/test.yml/badge.svg)](https://github.com/Panquesito7/setup-jule/actions/workflows/test.yml)

Easily setup a [JuleC](https://jule.dev) development environment in your project with GitHub Actions.\
Very useful when your project is built in the Jule programming language.

## Usage

Here's a basic workflow usage that you can use.\
For full information, check out [`action.yml`](https://github.com/Panquesito7/setup-jule/blob/main/action.yml).

```yml
name: Setup Jule
on: [push]
jobs:
  jule:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: Panquesito7/setup-jule@v1.0.0
        with:
          version: latest         # https://github.com/julelang/jule/releases for all JuleC versions.
          directory: .            # The directory where JuleC will be installed.
          architecture: amd64     # Architecture that will be used. Valid options are `amd64` and `arm64` (optional).
          add-to-path: false      # Whether to add JuleC to the PATH or not (optional).
          extra-command: version  # Extra command that will be run after compiling JuleC (optional; see below for more information).
```

### Version syntax

Release syntax is taken from the official [JuleC releases](https://github.com/julelang/jule/releases).

- `latest` and `current` for the latest release.
- `dev` for the latest commit.
- `beta-0.x.x` (there are no stable releases for now).

### Architecture

The given architecture that will be used to install JuleC.\
`arm64` and `amd64` can be used. `amd64` is the recommended architecture.

### Extra command

Extra command that will be run after compiling and installing JuleC.\
Here's a list of all available commands, as of `beta-0.0.2`:

- `version`: Prints the current version of JuleC. E.g.: `beta-0.0.2`.
- `help`: Prints all the available commands.
- `tools`: Extra tools that can be used with JuleC. Currently, seems undocumented.
- `julenv`: Shows information about the current JuleC environment.

```yml
- uses: actions/checkout@v3
- uses: Panquesito7/setup-jule@v1.0.0
  with:
    version: beta-0.0.2
    directory: ./libs
    architecture: amd64
    add-to-path: true
    extra-command: julenv
```

## Supported operating systems

Currently, macOS and Linux are supported, just like JuleC itself.\
Windows support will be added once JuleC supports Windows.

For more information: <https://github.com/julelang/jule/issues/34>

## License

See the [`LICENSE.md`](https://github.com/Panquesito7/setup-jule/blob/main/LICENSE.md) file for more information.
