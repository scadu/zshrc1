# Zebrafish Customization

Zebrafish is designed to provide a great turnkey experience out-of-the-box, but also to
allow you to customize it to your liking. This document describes the different ways you
might want to customize your Zebrafish experience.

- [Zebrafish Customization](#zebrafish-customization)
  - [Disable features](#disable-features)
  - [Adding plugins](#adding-plugins)
  - [Paths](#paths)
    - [History file](#history-file)
    - [compinit dump file](#compinit-dump-file)
    - [zshrc.d directory](#zshrcd-directory)
    - [zfunctions directory](#zfunctions-directory)
    - [zcompletions directory](#zcompletions-directory)
  - [Use a different plugin manager](#use-a-different-plugin-manager)
  - [Use on a server](#use-on-a-server)
  - [Customizing your prompt](#customizing-your-prompt)
  - [Using a different prompt](#using-a-different-prompt)

## Disable features

You can chose to disable certain features by setting the following `zstyle`. Perhaps
you are already using a plugin manager and don't want Zebrafish to load any plugins.

```zsh
# set this zstyle in your .zshrc before sourcing Zebrafish to disable features
zstyle ':zebrafish:disable' features plugins
```

The `$zf_features` variable contains everything that's currently enabled in Zebrafish
if you want to see the list of what you can disable, or refer to this readme.

## Adding plugins

Zebrafish gives you a small set of essential plugins, but you will likely want to add
your own. That's no problem! Zebrafish gives you total control of the plugin list.
Just set this `zstyle` before sourcing Zebrafish.

**Note** - you'll want to include the [zsh-defer] before any plugins you want to load
faster. If you have a plugin you don't want to defer, list it before [zsh-defer].

```zsh
# Make a list of the github plugins you want
myplugins=(
  # include zsh-defer before other plugins for rapid loading
  romkatv/zsh-defer
  # keep these standard Zebrafish plugins
  zsh-users/zsh-autosuggestions
  zsh-users/zsh-history-substring-search
  # add new favorites to my plugin list
  zsh-users/zsh-completions
  zshzoo/copier
  peterhurford/up.zsh
  rupa/z
  # plugins from other git providers
  https://gitlab.com/code-stats/code-stats-zsh
  # always load this one last
  zdharma-continuum/fast-syntax-highlighting
)

# assign that list to the appropriate zstyle
zstyle ':zebrafish:external' plugins $myplugins
```

## Paths

Many other shells like [fish] store data and cache files in separate locations from your
configs. Separating these location helps with things like storing your Zsh configuration
in a git repository without unintentially committing or deleting things you didn't mean
to. Zebrafish follows these concepts and respects the
[XDG base directory specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

The relevant directories are as follows:

| variable           | typical path(s)                       |
| ------------------ | ------------------------------------- |
| `$XDG_CONFIG_HOME` | `~/.config`                           |
| `$XDG_DATA_HOME`   | `~/.local/share`                      |
| `$XDG_CACHE_HOME`  | `~/.cache`                            |
| `$ZDOTDIR`         | `~/.config/zsh`, `~/.zsh`, or `$HOME` |

If you prefer to set your own paths, you can and Zebrafish will respect them.

### History file

Zebrafish will store your Zsh history file in `$XDG_DATA_HOME/zsh/zsh_history`. If you
don't prefer this, you can restore your zsh_history file to the Zsh default location or
wherever else you want by setting the `$HISTFILE` variable.

```zsh
HISTFILE=${ZDOTDIR:-~}/.zsh_history
```

### compinit dump file

Zebrafish will store your zcompdump file in `$XDG_CACHE_HOME/zsh/zcompdump`. If you
don't prefer this, you can restore your zcompdump file to the Zsh default location or
wherever else you want by setting the `$ZSH_COMPDUMP` variable.

```zsh
ZSH_COMPDUMP=${ZDOTDIR:-~}/.zcompdump
```

### zshrc.d directory

Zebrafish will source config files from `${ZDOTDIR:-$XDG_CONFIG_HOME/zsh}/zshrc.d` if it
exists. If you prefer to store config files in another location, you can set the
following `zstyle`:

```zsh
# replace ~/.zconf.d with whatever you want
zstyle ':zebrafish:zshrc.d' path ~/.zconf.d
```

### zfunctions directory

Zebrafish will autoload all function files in `${ZDOTDIR:-~/.config/zsh}/functions` if
it exists. If you prefer to store autoload function files in another location, you can
set the following `zstyle`:

```zsh
# replace ~/.zfunctions with whatever you want
zstyle ':zebrafish:zfunctions' path ~/.zfunctions
```

### zcompletions directory

Zebrafish will source completions files from `${ZDOTDIR:-~/.config/zsh}/completions` if
it exists. If you prefer to store completion files in another location, you can set the
following `zstyle`:

```zsh
# replace ~/.zcompletions with whatever you want
zstyle ':zebrafish:zcompletions' path ~/.zcompletions
```

### Plugins directory

Zebrafish will store plugins in `${ZDOTDIR:-~/.config/zsh}/plugins`. If you prefer to
store plugins in another location, you can set the following `zstyle`:

```zsh
# replace ~/.zplugins with whatever you want
zstyle ':zebrafish:plugins' path ~/.zplugins
```

## Use a different plugin manager

Zebrafish already comes with a highly performant way to manage plugins, but if you
prefer to use something else simply disable the 'plugins' feature.

```zsh
# disable the plugins feature
# (you can disable other features in this list too)
disable_features=(plugins)
zstyle ':zebrafish:disable' features $disable_features
```

## Use on a server

Zebrafish is great for use on a server since it's just a single .zsh file. But, in a
server environment, you might not want Zebrafish to try to go out to the internet
and grab plugins or the [Starship][starship] prompt. You can easily run Zebrafish in an
isolated environment by disabling these features:

```zsh
# disable any features that grab stuff from the web
# because you might not want that on a server
zstyle ':zebrafish:disable' features \
  prompt \
  plugins
```

## Customizing your prompt

Zebrafish uses the [Starship][starship] prompt. The Starship configuration file is
specified in the `$STARSHIP_CONFIG` variable, which defaults to
`~/.config/starship/zebrafish.toml`.

You can point `$STARSHIP_CONFIG` to another file, or you can modify the `zebrafish.toml`
file yourself. Configuration instructions for Starship [can be found here](https://starship.rs/config/).

## Using a different prompt

If you prefer to use a prompt other than [Starship][starship], you can disable the
Zebrafish prompt, and include your preferred prompt in the plugins list.

```zsh
# disable the Zebrafish prompt
zstyle ':zebrafish:disable' features prompt

# Example using the romkatv/powerlevel10k prompt plugin
# another popular prompt plugin is sindresorhus/pure
plugins=(
  romkatv/powerlevel10k
  romkatv/zsh-defer
  zsh-users/zsh-autosuggestions
  zsh-users/zsh-history-substring-search
  zsh-users/zsh-syntax-highlighting
)
zstyle ':zebrafish:external' plugins $plugins
```
