# Ubuntu
# Termux
```shell
pkg install proot-distro
# proot-distro install ubuntu, or shorthand:
pd i ubuntu
# proot-distro login ubuntu
pd sh ubuntu

pkg install zsh
chsh -s zsh


pkg install neovim -yq

pkg install tur-repo
pkg install code-server

pkg install chezmoi

pkg i uv

pkg install gh

pkg install termux-api  # Requires separate app to work. This enables clipboard in nvim

cargo install --locked tree-sitter-cli
pkg i ruff  # Mason installed ruff breaks on wheel build



```

# NeoVim
NeoVim is a terminal text editor that can be customized as a terminal IDE. It's a great alternative to PyCharm or VS Code

NeoVim has many out of the box configs (aka distro) and yhey can be installed and used in parallel with aliases[^*]:
```shell
# ~/.zshrc or ~/.oh-my-zsh/custom/aliases.zsh
alias v='nvim' # default Neovim config
alias vz='NVIM_APPNAME=nvim-lazyvim nvim' # LazyVim
alias vc='NVIM_APPNAME=nvim-nvchad nvim' # NvChad
alias vk='NVIM_APPNAME=nvim-kickstart nvim' # Kickstart
alias va='NVIM_APPNAME=nvim-astrovim nvim' # AstroVim
alias vl='NVIM_APPNAME=nvim-lunarvim nvim' # LunarVim
```
^* - https://michaeluloth.com/neovim-switch-configs/

# Known Issues
## Problems setting `zsh` as standard shell
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
