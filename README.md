## Shell Environment Setup

This guide provides instructions for setting up my development shell
environment. It's tailored to my personal preferences and requirements, but feel
free to use it as a foundation to create your own customized setup.

### 1. Installing ZSH

There are two main ways to install Zsh:

- With the package manager of your choice, e.g. `sudo apt install zsh`.
- From the source by following
  [the instructions from the Zsh FAQ](https://zsh.sourceforge.io/FAQ/zshfaq01.html#l7)

Once installed, verify installation by running `zsh --version`.

Finally, to make it your default shell run `chsh -s $(which zsh)`.

### 2. Installing a Package Manager

In order to install and manage ZSH plugins, we're using `zinit` package manager.

To install follow the instructions on their
[official repository](https://github.com/zdharma-continuum/zinit).

\* The recommendation is to follow the manual installation, so that your
`.zshrc` config can be more organized.

### 3. Installing a Nerd Font

In order for all glyphs to work, you need to make sure to install one of the
Nerd Font options available on their [website] (https://www.nerdfonts.com/).

\* The recommended font is `Jetbrains Mono`.

### 4. Installing Oh My Posh

Follow the guide on their
[official website](https://ohmyposh.dev/docs/installation/linux).

To add the prompt customizations, copy the `prompt.toml` file to
`~/.config/ohmyposh/`.

Then, include into your `.zshrc` file the following:

```shell
# Prompt
eval "$(oh-my-posh init zsh --config $HOME/.config/ohmyposh/prompt.toml)"
```

### 5. Installing `zinit` core plugins

\* For the last plugin to work properly, first make sure to to have **manually**
intalled [`fzf`](https://github.com/junegunn/fzf), and have included the
following to your `.zshrc` config:

```shell
# Source/Load fzf
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
```

Once that is done, to get the most of your shell, include the followig lines in
your `.zshrc`:

```shell
# Add in zsh plugins
zinit light zsh-users/zsh-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions
zinit light Aloxaf/fzf-tab

# Load Completions
autoload -Uz compinit && compinit

zinit cdreplay -q
```

This will install all the required plugins to enable shell auto completions and
a good syntax highlighting.

We can also include some snippets available on `Oh My Zsh` by including
`zinit snippet OMZL::<pluging-name>` line in your config.

Here, we will include `git` aliases:

```shell
# Add in snippets
zinit snippet OMZL::git.zsh
zinit snippet OMZP::git
```

For more plugins, check their
[official plugin list](https://github.com/ohmyzsh/ohmyzsh/wiki/plugins).

Finally, to ensure your auto completions menu uses the emacs keybindings as well
as correcting some search behaviors, include the following to `.zshrc`:

```shell
# Keybindings
bindkey -e
bindkey '^p' history-search-backward
bindkey '^n' history-search-forward
bindkey '^[w' kill-region
```

### 6. Configuring Auto Completions

To enhance the auto completions functionality, include the following lines in
your `.zshrc`:

```shell
# History
HISTSIZE=5000
HISTFILE=~/.zsh_history
SAVEHIST=$HISTSIZE
HISTDUP=erase
setopt appendhistory
setopt sharehistory
setopt hist_ignore_space
setopt hist_ignore_all_dups
setopt hist_save_no_dups
setopt hist_ignore_dups
setopt hist_find_no_dups
```

Then, include the following styling options to enhance the layout and behavior
of the auto completions:

```shell
# Completion Styling
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
zstyle ':completion:*' menu no
zstyle ':fzf-tab:complete:cd:*' fzf-preview 'ls --color $realpath'
zstyle ':fzf-tab:complete:__zoxide_z:*' fzf-preview 'ls --color $realpath'
```

### 7. Better Shell:

The default CLI commands can be improved by installing a few alternatives:

- [bat](https://github.com/sharkdp/bat)
- [eza](https://github.com/eza-community/eza)
- [fd](https://github.com/sharkdp/fd)

Then setup the following aliases and path in `.zshrc`:

```shell
# Path
export PATH="$PATH:$HOME/.local/bin"

# Aliases
alias cat="bat"
alias ls="eza"
alias la="eza -a"
```

As for the programming languages version manager, install the following:

- [asdf](https://github.com/asdf-vm/asdf)

Finally, to initialize `asdf` at startup, include the following lines:

```shell
# Source/Load asdf
. "$HOME/.asdf/asdf.sh"
```

### 8. Extra Aliases:

There are a few more aliases to include in order to make the navigation via the
CLI more plesant, for example:

```shell
# Aliases
alias c="clear"
```

### 9. Install Zoxide

Follow the instructions from the official repo:
https://github.com/ajeetdsouza/zoxide.

Once that is ready, add `eval "$(zoxide init --cmd cd zsh)"` to the end of
`~/.zshrc` file.

### 10. SSH Agent

In order for your SSH agent to start when you shell is being loaded, include the
following at the very start of your `~/.zshrc` file:

```shell
# Start ssh agent on load
eval "$(ssh-agent -s)" && clear
```

## Licence

This is an open-source project and is available under the
[**MIT License**](LICENSE). You are free to use, modify, and distribute the code
in accordance with the terms of the license.

## Contributors

Contributions are highly appreciated! If you encounter any issues or have
suggestions for improvements, please feel free to open an issue or submit a pull
request.

[feliperdamaceno](https://github.com/feliperdamaceno)

## Contact me

Linkedin: [feliperdamaceno](https://www.linkedin.com/in/feliperdamaceno)
