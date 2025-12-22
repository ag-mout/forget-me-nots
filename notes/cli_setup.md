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


```
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
