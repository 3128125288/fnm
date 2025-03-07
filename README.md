<h1 align="center">
  Fast Node Manager (<code>fnm</code>)
  <img alt="Amount of downloads" src="https://img.shields.io/github/downloads/Schniz/fnm/total.svg?style=flat" />
  <a href="https://dev.azure.com/galstar0385/fnm/_build/latest?definitionId=1?branchName=master"><img alt="Build Status" src="https://dev.azure.com/galstar0385/fnm/_apis/build/status/Schniz.fnm?branchName=master" /></a>
</h1>

> :rocket: Fast and simple Node.js version manager, built in native ReasonML

<div align="center">
  <img src="./docs/fnm.svg" alt="Blazing fast!">
</div>

## Features

:sparkles: Single file, easy installation, instant startup

:rocket: Built with speed in mind

:thinking: Works with `.nvmrc` and `.node-version` files

## Installation

### Using Homebrew (OSX)

```bash
brew install Schniz/tap/fnm
```

[This is a custom tap I'm maintaining](https://github.com/Schniz/homebrew-tap), and will be used until fnm will move to the official one.

### Using a script

For `bash`, `zsh` and `fish` shells, there's an [automatic installation script](./.ci/install.sh):

```bash
curl -fsSL https://github.com/Schniz/fnm/raw/master/.ci/install.sh | bash
```

### Upgrade

Upgrading `fnm` is almost the same as installing it. To prevent duplication in your shell config file add `--skip-shell` to install command.

#### Parameters

`--install-dir`

Set a custom directory for fnm to be installed. The default is `$HOME/.fnm`.

`--skip-shell`

Skip appending shell specific loader to shell config file, based on the current user shell, defined in `$SHELL`. e.g. for Bash, `$HOME/.bashrc`. `$HOME/.zshrc` for Zsh. For Fish - `$HOME/.config/fish/config.fish`

`--force-install`

MacOS installations using the installation script are deprecated in favor of the Homebrew formula, but this forces the script to install using it anyway.

Example:

```bash
curl -fsSL https://github.com/Schniz/fnm/raw/master/.ci/install.sh | bash -s -- --install-dir "./.fnm" --skip-shell
```

### Manually

- Download the [latest release binary](https://github.com/Schniz/fnm/releases) for your system
- Make it available globally on `$PATH`
- Add the following line to your `.bashrc`/`.zshrc` file:

  ```bash
  eval "`fnm env --multi`"
  ```

  If you are using [fish shell](https://fishshell.com/), add this line to your `config.fish` file:

  ```fish
  fnm env --multi | source
  ```

## Usage

You can always use `fnm --help` to read the docs:

### `fnm install [VERSION]`

Installs `[VERSION]`. If no version provided, it will install the version specified in the `.nvmrc` file located in the current working directory.

### `fnm use [VERSION]`

Activates `[VERSION]` as the current Node version. If no version provided, it will activate the version specified in the `.nvmrc` or `.node-version` file located in the current working directory.

### `fnm ls`

Lists the installed Node versions.

### `fnm ls-remote`

Lists the Node versions available to download remotely.

### `fnm alias [VERSION] [NAME]`

Aliases a Node version to a given name.

### `fnm default [VERSION]`

Aliases a Node version as default. Uses `fnm alias` underneath.

### `fnm env [--multi] [--shell=fish|bash|zsh] [--node-dist-mirror=URI] [--use-on-cd] [--fnm-dir=DIR] [--log-level=quiet|error|all]`

Prints the required shell commands in order to configure your shell, Bash compliant by default.

- Providing `--multi` will output the multishell support, allowing a different current Node version per shell
- Providing `--shell=fish` will output the Fish-compliant version. Omitting it and `fnm` will try to infer the current shell based on the process tree
- Providing `--node-dist-mirror="https://npm.taobao.org/dist"` will use the Chinese mirror of Node.js
- Providing `--use-on-cd` will also output a script that will automatically change the node version if a `.nvmrc`/`.node-version` file is found
- Providing `--fnm-dir="/tmp/fnm"` will install and use versions in `/tmp/fnm` directory

## Future Plans

- [ ] Feature: `fnm use --install`
- [ ] Linux: Replace `tar` with a statically linked library too (for ungzip + untar)
- [ ] Windows Support? @ulrikstrid has worked hard to make it compile on Windows, but it will probably need to have different code paths and logic. We can probably make another program and share feature tests with it, instead of relying on Windows for this very-unixy binary.

## Contributing

PRs welcome :tada:

### Developing:

```
npm install -g esy
git clone https://github.com/Schniz/fnm.git
cd fnm/
esy install
esy bootstrap
esy build
```

### Running Binary:

After building the project, you can run the main binary that is produced.

```
esy x fnm.exe
```

### Running Tests:

```
# Runs some smoke-unity test
esy test

# Runs the feature tests
feature_tests/run.sh
```
