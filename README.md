# macOS dev environment setup

## Security

### Hard disc encryption

Go to `System Preferences > Security & Privacy > FileVault` and make sure the FileVault is ON.

### Firewall

Go to `System Preferences > Security & Privacy > Firewall` and make sure the Firewall is ON.

### Require password after sleep

Go to `System Preferences > Security & Privacy > General` and set `Require password after sleep or screen saver begins`
to `immediately` or `5 seconds`.

### More

* https://blog.bejarano.io/hardening-macos.html
* https://github.com/drduh/macOS-Security-and-Privacy-Guide

## Keyboard preferences

In `System preferences > Keyboard`:

  * `Key Repeat > Fast` (all the way to the right)
  * `Delay Until Repeat > Short` (all the way to the right)
  * `Modifier Keys... > Caps Lock (⇪) Key` set to `^ Control`

## Apps

### Text editor

Install VS Code: https://code.visualstudio.com/

#### Configuration

Open VS Code, go to `Code` > `Preferences` > `Settings` and paste:

```yml
{
    "editor.rulers": [
        120
    ],
    "editor.tabSize": 2,
    "explorer.confirmDragAndDrop": false,
    "explorer.confirmDelete": false,
    "workbench.startupEditor": "newUntitledFile",
    "files.insertFinalNewline": true,
    "files.trimTrailingWhitespace": true,
    "files.trimFinalNewlines": true,
    "terminal.integrated.fontFamily": "Meslo LG S DZ for Powerline",
}
```

### Web browser

Install Chrome: https://www.google.com/chrome/browser/desktop/index.html

#### Extensions I recommend

##### Security / privacy

* [ublock-origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm)
* [https-everywhere](https://chrome.google.com/webstore/detail/https-everywhere/gcbommkclmclpchllfjekcdonpmejbdp)
* [privacy-badger](https://chrome.google.com/webstore/detail/privacy-badger/pkehgijcmpdhfbdbbnkijodmdjhbjlgp)

##### Utilities

* [full-page-screen-capture](https://chrome.google.com/webstore/detail/full-page-screen-capture/fdpohaocaechififmbbbbbknoalclacl)

### Terminal

Install iTerm2: https://www.iterm2.com/downloads.html

### Software package manager

Install Homebrew: http://brew.sh/

### Basic tools

Install some useful packages:

```shell
brew install curl mc
```

### Git

Install Git:

```shell
brew install git
```

Set you username and email in Git:

```shell
git config --global user.name "Mona Lisa"
git config --global user.email "email@example.com"
```

:warning: Don't forget to replace _"Mona Lisa"_ and _"email@example.com"_ with your own data.

### Shell

Install [Zsh] and set it as a default shell:

```shell
brew install zsh zsh-completions
chsh -s /bin/zsh
```

:warning: Reopen terminal window now to load Zsh shell.

Install [Oh My Zsh]:

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Make your terminal look pretty

#### Use Dark Background in iTerm2

* Go to: `iTerm2 > Preferences > Profiles > Colors`
* Use `Color presets...` menu to import and select downloaded `Pastel (Dark Background)` theme

#### Install [Powerline Fonts]

```shell
cd $HOME
git clone https://github.com/powerline/fonts.git
./fonts/install.sh
rm -rf ~/fonts/
```

#### Set font in iTerm2

* Go to: `iTerm2 > Preferences > Profiles > Text > Font > Change Font`
* Select the font: `Fixed Width > Meslo LG S DZ for Powerline > RegularForPowerline > 11`

#### Set [zsh theme]

Edit `~/.zshrc` file and update `ZSH_THEME=` to:

```shell
ZSH_THEME="agnoster"
```

### Configure Zsh

Install [zsh-autosuggestions]:

```shell
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

Edit `~/.zshrc` file and update `plugins=` to:

```shell
plugins=(git rails zsh-autosuggestions)
```

:mortar_board: List of all available plugins is here: https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins.

Edit `~/.zshrc` file and the following lines at the end:

```shell
export EDITOR='vim'

DEFAULT_USER=`whoami`

HISTFILE=$HOME/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
setopt APPEND_HISTORY           # append rather than overwrite history file.
setopt EXTENDED_HISTORY         # save timestamp and runtime information
setopt HIST_EXPIRE_DUPS_FIRST   # allow dups, but expire old ones when I hit HISTSIZE
setopt HIST_FIND_NO_DUPS        # don't find duplicates in history
setopt HIST_IGNORE_ALL_DUPS     # ignore duplicate commands regardless of commands in between
setopt HIST_IGNORE_DUPS         # ignore duplicate commands
setopt HIST_REDUCE_BLANKS       # leave blanks out
setopt HIST_SAVE_NO_DUPS        # don't save duplicates
setopt INC_APPEND_HISTORY       # write after each command
setopt SHARE_HISTORY            # share history between sessions

ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=30'

export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# homebrew
export HOMEBREW_NO_INSECURE_REDIRECT=1
export HOMEBREW_CASK_OPTS=--require-sha
```

### Vim

Install [Janus Vim Distribution]:

```shell
curl -L https://bit.ly/janus-bootstrap | bash
```

Map `jj` to `esc`:

```shell
echo ':imap jj <Esc>' >> ~/.vimrc.before
```

### GPG Suite

https://gpgtools.org/#gpgsuite

### Another apps I recommend

* [Spectacle](https://www.spectacleapp.com/)
* [Monosnap](https://monosnap.com/welcome)
* [Alfred](https://www.alfredapp.com/)
* [GitHub Desktop](https://desktop.github.com/)
* [MenuMeters](https://member.ipmu.jp/yuji.tachikawa/MenuMetersElCapitan/)

### RoR & web development

#### PostgreSQL

```shell
brew install postgresql
brew services start postgresql
```

#### Redis

```shell
brew install redis
brew services start redis
```

#### Version Manager with support for Ruby, Node.js, Elixir, Erlang & more

Install [asdf-vm](https://asdf-vm.com/#/core-manage-asdf-vm):

```shell
brew install asdf
echo -e "\n. $(brew --prefix asdf)/asdf.sh" >> ~/.zshrc
echo -e "\n. $(brew --prefix asdf)/etc/bash_completion.d/asdf.bash" >> ~/.zshrc
```

##### Install multiple languages

```shell
# install last version of Ruby
asdf plugin-add ruby
asdf install ruby 2.6.5
asdf global ruby 2.6.5

# install last version of Erlang & Elixir
asdf plugin-add erlang
asdf install erlang 22.1.5
asdf global erlang 22.1.5
asdf plugin-add elixir
asdf install elixir 1.9.4
asdf global elixir 1.9.4

# install last version of Node JS
asdf plugin-add nodejs
asdf install nodejs 13.0.1
asdf global nodejs 13.0.1
```

```shell
# to display the list of available versions, use `list-all`, ex:
asdf list-all ruby
```

[Zsh]: http://www.zsh.org/
[Oh My Zsh]: https://github.com/robbyrussell/oh-my-zsh
[Powerline Fonts]: https://github.com/powerline/fonts
[zsh theme]: https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
[zsh-autosuggestions]: https://github.com/zsh-users/zsh-autosuggestions
[Janus Vim Distribution]: https://github.com/carlhuda/janus
