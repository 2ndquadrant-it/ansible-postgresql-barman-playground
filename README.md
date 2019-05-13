# ansible-postgresql-barman-playground

Playground environment for PostgreSQL and Barman that uses Vagrant and Ansible.

## Requirements

- Vagrant
- VirtualBox
- pyenv
- Ansible

Developed and tested on Mac OS X with VirtualBox 6, Vagrant 2.2.4 and Ansible 2.7.5.
Installed using `homebrew` with:

```
brew install pyenv pyenv-virtualenv
brew cask install virtualbox vagrant
```

## Installing Ansible using pyenv

To install Python 3 on your system using pyenv, follow the instructions you find
on the [pyenv](https://github.com/pyenv/pyenv) and [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
projects.

A typical installation process (assuming 3.7.3 is the latest stable version) would look like:

```bash
pyenv install 3.7.3
pyenv virtualenv 3.7.3 pg-playground
pyenv local pg-playground
pip install -r requirements.txt
```
