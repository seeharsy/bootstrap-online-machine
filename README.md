# Configure New Ubuntu or Fedora Host

This playbook automates the installation of a variety of useful
packages and utilities for a freshly installed instance of Ubuntu
Desktop or Fedora Workstation. The list of optional utilities
installed are:

- Docker
- 1Password
- Mattermost Desktop
- VS Code (and some useful extensions)
- Yubico Authenticator App
- Chrome, Firefox and Chromium browsers

## Requirements

- Ensure the host has access to the internet, unrestricted by a
  firewall or proxy
- This playbook has only been tested on Ubuntu and Fedora distros.
  All other distros may encounter issues when running this playbook
  - **Disclaimer:** Fedora 41 is currently not compatible and may
    not work as expected
- If running this playbook locally, Ansible will need to be installed:
  - For Debian-based distros, use `sudo apt install ansible-core`
  - Otherwise on Fedora-based distros, use `sudo dnf install ansible-core`

## Role Variables

A list of packages to be installed can be found in `defaults/main.yml`.
This list can be added to as desired, but removal of any packages may cause
issues with the installation of the utilities.

## Dependencies

This playbook requires the following Ansible Galaxy role and collection to be
installed:

- `ansible-galaxy install geerlingguy.docker`
- `ansible-galaxy collection install community.general`

## Usage

An example playbook has been included `configure_online_machine.yml`.

- To run this over a remote host: `ansible-playbook -i path/to/hosts/file configure_online_laptop.yml -K`
  . Ensure you use `--limit` and select only the desired hosts.
- To run this locally: `ansible-playbook --connection=local -i 127.0.0.1, configure_online_laptop.yml -K`

Since the playbook handles installation of packages, the `-K` option is needed
to pass a privilege escalation password.

Ansible tags are being used to specify which of the utilities are being used.
The common packages are always going to be installed and updated, but you can
specify whether or not you want to install VS Code, Docker, Mattermost etc.
by using `--tags=vscode,docker,mattermost`.

## License

BSD
