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
      - uses: Panquesito7/setup-jule@v1.2.0
        with:
          version: latest         # https://github.com/julelang/jule/releases for all JuleC versions.
          directory: .            # The directory where JuleC will be installed.
          architecture: amd64     # Architecture that will be used. Valid options are `amd64`, `arm64`, and `i386` (Windows/Linux only; optional).
          add-to-path: false      # Whether to add JuleC to the PATH or not (optional).
          extra-command: version  # Extra command that will be run after compiling JuleC (optional; see below for more information).
```

### Version syntax

Release syntax is taken from the official [JuleC releases](https://github.com/julelang/jule/releases).

- `latest` and `current` for the latest release.
- `dev` for the latest commit.
- `beta-0.x.x` (there are no stable releases for now).

### Architecture

The architecture that will be used to install JuleC.\
`arm64`, `amd64`, and `i386` (Windows/Linux only) can be used. `amd64` is the recommended architecture.

### Extra command

An extra command will be run after compiling and installing JuleC.\
You can see the full list of commands in the [official manual](https://manual.jule.dev/compiler/basic-commands.html).

> **Note**
>
> The manual is updated and based on the latest Jule commits.\
> However, the IR file might not be up-to-date, meaning that new commands won't work.

```yml
- uses: actions/checkout@v3
- uses: Panquesito7/setup-jule@v1.2.0
  with:
    version: beta-0.0.3
    directory: ./libs
    architecture: amd64
    add-to-path: true
    extra-command: version
```

## Supported operating systems

All the major operating systems are supported, being **Windows**, **Linux**, and **macOS**.\
You can easily compile Jule code in all OSes or specific ones by changing the operating system.

In this example, the action will run in the three operating systems.

```yml
...
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macOS-latest, windows-latest]
    steps:
      - uses: actions/checkout@v3
      - name: Setup Jule
        uses: Panquesito7/setup-jule@v1.2.0
        with:
          version: dev
          directory: .
          add-to-path: true
...
```

## License

See the [`LICENSE.md`](https://github.com/Panquesito7/setup-jule/blob/main/LICENSE.md) file for more information.
