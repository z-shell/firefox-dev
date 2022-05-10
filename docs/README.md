
<h1></h1><div align="center"><table>
  <tr><td align="center">
  <a title="ZI" target="_self" href="https://github.com/z-shell/zi/">
    <h2><img align="center" style="width:60px;height:auto" src="https://github.com/z-shell/zi/raw/main/docs/images/logo.svg" alt="ZI Logo" /></a>
❮ ZI ❯ Package - Firefox Developer Edition </h2>
    <h3> Install and setup the latest binary of Mozilla Firefox Deveveloper Edition </h3>
  </td></tr>
  <tr><td align="center">
  <h2>
  
| **Package source:** | Source Tarball |            Binary            | Git | Node | Gem |
| :-----------------: | :------------: | :--------------------------: | :-: | :--: | :-: |
|     **Status:**     |      :x:       | :heavy_check_mark: (default) | :x: | :x:  | :x: |

  </h2><img style="width:100%;height:auto" src="https://user-images.githubusercontent.com/59910950/161095968-8f10a351-9fc1-412a-903c-b3eeed601c71.gif" alt="Preview" /></td></tr></table></div>

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

Provides the CLI commands `firefox-bin` and `firefox` by extending the `$PATH`
to point to the snippet's directory.

The command executed will be equivalent to:

```zsh
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

```zsh
zi id-as"firefox-dev" as"null" lucid \
  atclone'local ext="${${${(M)OSTYPE#linux*}:+tar.bz2}:-dmg}"; \
    ziextract %ID% $ext --norm ${${OSTYPE:#darwin*}:+--move}' \
      atpull"%atclone" nocompile is-snippet for \
         "https://download.mozilla.org/?product=firefox-devedition-latest-ssl&os=${${${(M)OSTYPE##linux}:+linux64}:-${${(M)OSTYPE##darwin}:+osx}}&lang=en-US"
```

---
 
> This repository compatible with [ZI](https://github.com/z-shell/zi)

The [Mozilla Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) zsh package that can use the NPM package registry to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.
