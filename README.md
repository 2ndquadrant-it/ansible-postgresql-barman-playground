# ansible-postgresql-barman-playground

Playground environment for PostgreSQL and Barman that uses Vagrant and Ansible.

## Requirements

- Vagrant
- VirtualBox
- pyenv
- Ansible

Developed and tested on Linux and Mac OS X with Ansible 2.8.5, VirtualBox 6, and Vagrant 2.2.5.

On Linux you can install them using your default package manager. On OS X, they can be installed using `homebrew`:

```
brew install pyenv pyenv-virtualenv
brew cask install virtualbox vagrant
```

## Installing Ansible using pyenv

To install Python 3 on your system using pyenv, follow the instructions you find
on the [pyenv](https://github.com/pyenv/pyenv) and [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
projects.

A typical installation process (assuming 3.7.4 is the latest stable version) will be similar to:

```bash
pyenv install 3.7.4
pyenv virtualenv 3.7.4 pg-playground
pyenv local pg-playground
pip install -r requirements.txt
```

## Hosts and inventory

There is a `Vagrantfile` present in this repository, which is used to quickly deploy 4 VMs, that are then used as target hosts for the playbook. So, as listed in the **Requiriments** section above, [Vagrant](https://www.vagrantup.com/) and [Virtualbox](https://www.virtualbox.org/wiki/Downloads) are expected to be already installed and working on your computer before running the playbook.

Running `vagrant up` will create the four VMs: `paul`, `john`, `george`, and `ringo`. Yes, you've probably already heard about those guys. ;)
These VM's are already listed in the inventory file at `inventory/inventory.ini`.

You can use the file `ssh_config`, located in the root of this repository, to be able to acces the VMs using their specific hostnames instead of their IP addresses if you prefer.


## Running the playbook

The playbook can be run as any Ansible playbook:

```bash
ansible-playbook pg_playground.yml
```

In case you want to run the playbook only on some of the hosts, you can use `-l` (`--limit`) to specify them:

```bash
ansible-playbook pg_playground.yml -l paul,ringo
```

By default, when running this complete, you will have 2 PostgreSQL masters and 2 Barman
server up and running independently. Communication through `SSH` should already be working
between the servers, so you can start your experiments, for example:

- setting one of the masters as a standby and implementing streaming replication between them
- configuring barman to be the backup manager of your new cluster
- pointing the standby to recover WAL files from barman, to be extra sure WALs will always be found
- set the other barman server as a secondary backup server, having another layer of redundancy
- etc, etc, etc...

We hope you have fun!
