# Setup laptop installation

I run these after reinstalling fedora and going through the initial setup
to create my user. Recently, I got really tired of doing things manually though, so here
comes automation.

## Requirements

Install ansible

```
sudo dnf install ansible ansible-collection-community-general
```

If needed, open and login through SSH (make sure you are in a private network beforehand?):

```
sudo firewall-cmd --add-service=ssh 
systemctl start sshd
```

## Setup system

### Base system configuration

 * set up system config with hostname, DNF and sysctl changes
 * enables RPM fusion and vscode repos
 * removes unused (or bothersome) packages installed by default
 * install base package set and media codes

```
ansible-playbook -bK setup-base.yaml --extra-vars "laptop_hostname=<laptop hostname>"
```

### User configuration

As the user configured on the laptop:

 * add flathub flatpak repo
 * install flatpaks from flathub
 * disable Gnome Software updates auto download
 * set up customized Gnome
 * set up PSD for RAM based browser profiles

```
ansible-playbook setup-user.yaml
```