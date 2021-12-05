<h3>

| **Package source:** | Source Tarball |            Binary            | Git | Node | Gem |
| :-----------------: | :------------: | :--------------------------: | :-: | :--: | :-: |
|     **Status:**     |      :x:       | :heavy_check_mark: (default) | :x: | :x:  | :x: |

</h3>

- [Introduction](#introduction)
- [Install](#install)
  - [Available `pack''` invocations](#available-pack-invocations)
  - [Default Profile](#default-profile)
  - [`Bin-Gem-Node` Profile](#bin-gem-node-profile)

## Introduction

> **[?]**
> This repository not compatible with previous versions (zplugin, zinit).
>
> Please upgrade to [ZI](https://github.com/z-shell-zi)

The [Mozilla Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) zsh package that can use the NPM package registry to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.

## Install

### Available `pack''` invocations

```zsh
# Download the binary of amazon-firefox-dev command
zi pack for firefox-dev

# Download the firefox-dev binary with use of the bin-gem-node annex
zi pack"bgn" for firefox-dev
```

### Default Profile

Provides the CLI commands `firefox-bin` and `firefox` by extending the `$PATH`
to point to the snippet's directory.

The ZI command executed will be equivalent to:

```zsh
zi id-as"firefox-dev" as"command" lucid" \
    atclone'local ext="${${${(M)OSTYPE#linux*}:+tar.bz2}:-dmg}"; \
        zpextract %ID% $ext --norm ${${OSTYPE:#darwin*}:+--move}'
    pick"firefox(|-bin)" atpull"%atclone" nocompile is-snippet for \
        "https://download.mozilla.org/?product=firefox-devedition-latest-ssl&os=${${${(M)OSTYPE##linux}:+linux64}:-${${(M)OSTYPE##darwin}:+osx}}&lang=en-US"
```

### `Bin-Gem-Node` Profile

Provides the CLI command `firefox` by creating a forwarder script (a _shim_) to
the `firefox-bin` command, in `$ZPFX/bin` by using the
[bin-gem-node](https://github.com/z-shell/z-a-bin-gem-node) annex. It's the best
method of providing the binary to the command line.

The ZI command executed will be equivalent to:

```zsh
zi id-as"firefox-dev" as"null" lucid \
    atclone'local ext="${${${(M)OSTYPE#linux*}:+tar.bz2}:-dmg}"; \
        zpextract %ID% $ext --norm ${${OSTYPE:#darwin*}:+--move}'
    atpull"%atclone" nocompile is-snippet for \
        "https://download.mozilla.org/?product=firefox-devedition-latest-ssl&os=${${${(M)OSTYPE##linux}:+linux64}:-${${(M)OSTYPE##darwin}:+osx}}&lang=en-US"
```
