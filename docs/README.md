<div align="center"><table><tr><td>
  <a target="_self" href="https://github.com/z-shell/zi/">
  <h1><img align="center" src="https://github.com/z-shell/zi/raw/main/docs/images/logo.svg" width="60px" height="60px" alt="ZI Logo" /></a>
  ❮ ZI ❯ Package - Firefox Developer Edition </h1>
<h2 align="center">

| **Package source:** | Source Tarball |            Binary            | Git | Node | Gem |
| :-----------------: | :------------: | :--------------------------: | :-: | :--: | :-: |
|     **Status:**     |      :x:       | :heavy_check_mark: (default) | :x: | :x:  | :x: |

</h2>
  <h3 align="center">
  <p> Install and setup the latest binary of Mozilla Firefox Deveveloper Edition </p>
  <p><img align="center" src="https://user-images.githubusercontent.com/59910950/161095968-8f10a351-9fc1-412a-903c-b3eeed601c71.gif" width="100%" height="auto" alt="zi package firefox-dev" /></p>
  </h3>
</td></tr></table></div><hr />

### Available `pack''` invocations

```shell
# Default Profile
zi pack for firefox-dev
```

```shell
# Download the firefox-dev binary with use of the bin-gem-node annex
zi pack"bgn" for firefox-dev
```

### Default Profile

Provides the CLI commands `firefox-bin` and `firefox` by extending the `$PATH` to point to the snippet's directory.

The command executed will be equivalent to:

```shell
zi id-as"firefox-dev" as"command" lucid" \
  atclone'local ext="${${${(M)OSTYPE#linux*}:+tar.bz2}:-dmg}"; \
    ziextract %ID% $ext --norm ${${OSTYPE:#darwin*}:+--move}' \
      pick"firefox(|-bin)" atpull"%atclone" nocompile is-snippet for \
          "https://download.mozilla.org/?product=firefox-devedition-latest-ssl&os=${${${(M)OSTYPE##linux}:+linux64}:-${${(M)OSTYPE##darwin}:+osx}}&lang=en-US"
```

### `Bin-Gem-Node` Profile

Provides the CLI command `firefox` by creating a forwarder script (a _shim_) to the `firefox-bin` command, in `$ZPFX/bin` by using the [bin-gem-node](https://github.com/z-shell/z-a-bin-gem-node) annex.

It's the best method of providing the binary to the command line.

The command executed will be equivalent to:

```shell
zi id-as"firefox-dev" as"null" lucid \
  atclone'local ext="${${${(M)OSTYPE#linux*}:+tar.bz2}:-dmg}"; \
    ziextract %ID% $ext --norm ${${OSTYPE:#darwin*}:+--move}' \
      atpull"%atclone" nocompile is-snippet for \
         "https://download.mozilla.org/?product=firefox-devedition-latest-ssl&os=${${${(M)OSTYPE##linux}:+linux64}:-${${(M)OSTYPE##darwin}:+osx}}&lang=en-US"
```

---

> This repository compatible with [ZI](https://github.com/z-shell/zi)

The [Mozilla Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) zsh package that uses the [zsh-string-lib](https://github.com/z-shell/zsh-string-lib) to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.
