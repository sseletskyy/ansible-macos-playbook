# Ansible MacOS Playbook

This is the playbook I use after a clean install of MacOS to set everything up.

## Roles/Tasks

- Install ssh keys (Role `ssh`)
- Installs Homebrew packages and app casks (Role `homebrew`)
- Installs App Store apps with [`mas-cli`](https://github.com/mas-cli/mas) (Role `mas`)
- Modifies MacOS settings (Role `settings`)
- Install other homebrew packages with custom installation process, e.g. omz (Role `custombrew`)
- Stow .dotfiles (Role `custombrew`, task `dotfiles`)

## Installation

Clone a repo in the home dir
```shell
cd ~
git clone https://github.com/sseletskyy/ansible-macos-playbook.git
```

1. Install xcode

```shell
xcode-select --install
```

2. Install homebrew

```shell
cd ~
git clone https://github.com/Homebrew/brew homebrew
brew update -force --quiet
chmod -R go-w "$(brew --prefix)/share/zsh"
```

3. Install ansible

```shell
brew install python
pip3 install ansible
cd ~/ansible-macos-playbook
```

4. Run `ansible-playbook main.yml --verbose --ask-vault-pass`. Enter your account password when prompted. Enter vault password when prompted.

5. Or run specific role only 
```shell
# ssh
ansible-playbook main.yml -t ssh --verbose --ask-vault-pass

# homebrew
ansible-playbook main.yml -t homebrew --verbose

# mas (Macos App Store)
ansible-playbook main.yml -t mas --verbose

# settings
ansible-playbook main.yml -t settings --verbose

# custom homebrew
ansible-playbook main.yml -t custombrew --verbose
```
