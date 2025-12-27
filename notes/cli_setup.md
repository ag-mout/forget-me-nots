# CLI SETUP

## Ubuntu

```shell
sudo apt-get update && apt-get upgrade -y

apt install -y git curl wget tmux neovim ripgrep gh openssh-client nodejs rustc

pip install -yq uv
uv tool install ruff

sh -c "$(curl -fsLS get.chezmoi.io)"

apt install zsh
chsh -s zsh

```

```shell
GITHUB_USERNAME="ag-mout" chezmoi init git@github.com:$GITHUB_USERNAME/dotfiles.git

```

## Termux

```shell
pkg update && pkg upgrade -y

pkg install -y git curl wget openssh tmux neovim python nodejs-lts ripgrep fd marksman ruff chezmoi uv gh termux-api rust lazygit

pkg install zsh
chsh -s zsh

cargo install --locked tree-sitter-cli

```

It's also possible to install Linux distros with proot:

```shell
pkg install proot-distro

# proot-distro install ubuntu, or shorthand
pd i ubuntu

# proot-distro login ubuntu
pd sh ubuntu
```

To install VS Code another repo is required

```shell
pkg install tur-repo
pkg install code-server
```

### uv on Termux config

Termux has its own PyPi repo. Configuring uv to read from there will prevent some issues when a suitable wheel is not found.
Create the file `~/.config/uv/uv.toml`

```shell
mkdir -p ~/.config/uv && nvim ~/.config/uv/uv.toml
```

Add this to the config:

```toml
[[index]]
name = "termux"
url = "https://termux-user-repository.github.io/pypi/"
```

This may not be enough so set the environment variable to read the file:

```shell
~/.zshrc
~~~~~~~~
export UV_CONFIG_FILE="$HOME/.config/uv/uv.toml" 
~~~~~~~~
```

## NeoVim

NeoVim is a terminal text editor that can be customized as a terminal IDE. It's a great alternative to PyCharm or VS Code

> Installation should not be required because chezmoi is saving a copy of the configs

NeoVim has many out of the box configs (aka distro) and they can be installed and used in parallel with aliases[^*]:

```shell
# ~/.zshrc or ~/.oh-my-zsh/custom/aliases.zsh
alias v='nvim' # default Neovim config
alias vz='NVIM_APPNAME=nvim-lazyvim nvim' # LazyVim
alias vc='NVIM_APPNAME=nvim-nvchad nvim' # NvChad
alias vk='NVIM_APPNAME=nvim-kickstart nvim' # Kickstart
alias va='NVIM_APPNAME=nvim-astrovim nvim' # AstroVim
alias vl='NVIM_APPNAME=nvim-lunarvim nvim' # LunarVim
```

^* - <https://michaeluloth.com/neovim-switch-configs/>

### LazyVim IDE setup

On the LazyExtras choose these plugins for an IDE experience:

- lang.python
- lang.json
- lang.toml
- lang.markdown
- dap.core
- test.core
- editor.refactoring

^* - <https://dev.to/gitaroktato/configuring-lazyvim-and-python-on-windows-nke>

## Known Issues

### Problems setting `zsh` as standard shell

If the error `chsh: PAM: Authentication failure` pops up, the auth settings can be temporarily disabled to allow changing:

```shell
vim /etc/pam.d/chsh
# comment the line with: auth       required   pam_shells.so
# try to change again
chsh -s /path/to/zsh

# open the permissions file again to enable auth again
```

Check the current shell with:

```shell
echo $0
```
