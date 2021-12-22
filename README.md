# Zebrafish

[![MIT License](https://img.shields.io/badge/license-MIT-007EC7.svg)](/LICENSE)
![version](https://img.shields.io/badge/version-v0.7.0-orange)

<a title="Azul [Copyrighted free use], via Wikimedia Commons"
   href="https://commons.wikimedia.org/wiki/File:Zebrafisch.jpg"
   align="right">
<img align="right"
     width="250"
     alt="Zebrafish"
     src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/Zebrafisch.jpg/512px-Zebrafisch.jpg">
</a>

> A lightweight, full-featured, blazing-fast Zsh micro-framework. :zebra: :fish:

<br>
<br>

## TLDR;

Download Zebrafish and source it from your `.zshrc`:

```zsh
curl -fsSL https://git.io/zsh-zebrafish -o ${ZDOTDIR:-~}/.zebrafish.zsh
echo 'source ${ZDOTDIR:-~}/.zebrafish.zsh' >> ${ZDOTDIR:-~}/.zshrc
```

## Details

Zebrafish is what you might call a _micro-framework_ for Zsh. It's designed to be a
portable, lightweight, ultra-fast, full-featured Zsh configuration in a single file.
Equally useful on your desktop machine or on a remote server, Zebrafish brings many of
the goodies [found in other shells][fish] to your Zsh configuration. And, it's
ridiculously fast!

Zebrafish's goal is to give you a great DIY Zsh experience from a single file. Other
full Zsh Frameworks like [Oh-My-Zsh][ohmyzsh] and [Prezto][prezto] are nice if
you want everything-and-the-kitchen-sink, but you pay a performance and complexity
penalty for using these frameworks.

Many prefer to build their own Zsh config from scratch, but that can be a lot of work
and often requires you to pull together functionality already baked into the Zsh
frameworks you leave behind.

Zebrafish is simpler. Similar to [Grml's .zshrc][grml-zshrc], Zebrafish gives you
everything you need for a full-featured Zsh config, but encompassed in one simple to
grok Zsh include that will grow with you as you use Zsh.

Feel free to use it as-is, build off it, or fork it and make it entirely your own.

![zebrafish](https://raw.githubusercontent.com/mattmc3/zebrafish/resources/img/zebrafish.png)

## Features

| feature             | description                                                                |
| ------------------- | -------------------------------------------------------------------------- |
| environment         | Set common environment variables                                           |
| zshopts             | Better Zsh options than the defaults                                       |
| history             | Better Zsh history settings than the defaults                              |
| completion-styles   | Add zstyle completion options                                              |
| keybindings         | Add common key bindings                                                    |
| termtitle           | Set the terminal window title                                              |
| help                | Enable the Zsh built-in help                                               |
| colorized-man-pages | Add a splash of color to your man pages                                    |
| zfunctions          | Use a `functions` directory in `$ZDOTDIR` for your custom Zsh functions    |
| zshrcd              | Use a `zshrc.d` directory in `$ZDOTDIR` to load config files               |
| zcompletions        | Use a `completions` directory in `$ZDOTDIR` to add your custom completions |
| plugins             | Include external Zsh plugins from git repos                                |
| prompt              | Use the amazing [Starship][starship] prompt                                |
| compinit            | Initialize completions                                                     |

## Plugins

Zebrafish includes a few essential plugins:
- [zsh-defer](https://github.com/romkatv/zsh-defer)
- [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [history-substring-search](https://github.com/zsh-users/zsh-history-substring-search)
- [syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

## Installation

### Install as a single file

Grab the Zebrafish file via `curl`, and source it from your `.zshrc`:

```zsh
curl -fsSL https://git.io/zsh-zebrafish -o ${ZDOTDIR:-~}/.zebrafish.zsh
echo 'source ${ZDOTDIR:-~}/.zebrafish.zsh' >> ${ZDOTDIR:-~}/.zshrc
```

### Install from the git repository

Grab the Zebrafish repo via `git`, and source it from your `.zshrc`:

```zsh
git clone https://github.com/mattmc3/zebrafish ${ZDOTDIR:-~/.config/zsh}/plugins/zebrafish
echo 'source ${ZDOTDIR:-~/.config/zsh}/plugins/zebrafish/zebrafish.zsh' >> ${ZDOTDIR:-~}/.zshrc
```

### Install with a Zsh plugin manager

To install using a Zsh plugin manager, add the following to your .zshrc

- [pz]: `pz source mattmc3/zebrafish`
- [zcomet]: `zcomet load mattmc3/zebrafish`
- [zgenom]: `zgenom load mattmc3/zebrafish`
- [znap]: `znap source mattmc3/zebrafish`

Note that when using a plugin manager, you may prefer to turn off Zebrafish's built-in
plugin management with `zstyle ':zebrafish:disable' features plugins`.

## Customization

Zebrafish allows you to disable features you don't want or need, set paths to where you
prefer, change your prompt, add Zsh plugins, and many other changes to make it your own.

You can read more about how to customize your Zebrafish experience
[here](/docs/CUSTOMIZE.md).

## Performance

Zebrafish is blazing fast. In my tests it was 3 times faster than [prezto] and
nearly 5 times faster to load than [oh-my-zsh][ohmyzsh].

Zebrafish achieves much of its performance by being smaller and simpler than the big
frameworks. It also leverages the [zsh-defer] plugin to get you to a prompt faster. When
loading plugins, everything loaded after zsh-defer will use it to source your plugin.

You can test the speed of your Zsh config for yourself by running the following command:

```zsh
for i in $(seq 10); do
  /usr/bin/time zsh -i -c exit
done
```

![zebrafish](https://raw.githubusercontent.com/mattmc3/zebrafish/resources/img/benchmark.png)


[fish]: https://fishshell.com
[grml-zshrc]: https://github.com/grml/grml-etc-core/blob/master/etc/zsh/zshrc
[ohmyzsh]: https://github.com/ohmyzsh/ohmyzsh
[prezto]: https://github.com/sorin-ionescu/prezto
[pz]: https://github.com/mattmc3/pz
[starship]: https://starship.rs
[zcomet]: https://github.com/agkozak/zcomet
[zgenom]: https://github.com/jandamm/zgenom
[znap]: https://github.com/marlonrichert/zsh-snap
[zsh-defer]: https://github.com/romkatv/zsh-defer
[zsh-users]: https://github.com/zsh-users/
