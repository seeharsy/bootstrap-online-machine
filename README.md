# Configure New Ubuntu or Fedora Host

This playbook automates the installation of a variety of useful
packages and utilities for a freshly installed instance of Ubuntu
Desktop or Fedora Workstation. The list of optional utilities
installed are:

- Docker
- 1Password
- Mattermost Desktop (latest version fetched automatically)
- VS Code (and some useful extensions)
- Yubico Authenticator (latest version fetched automatically)
- Chrome, Firefox and Chromium browsers (with Browserpass CE extension)
- pass-otp (OTP extension for pass)

## Requirements

- Ensure the host has access to the internet, unrestricted by a
  firewall or proxy
- This playbook has only been tested on Ubuntu and Fedora distros.
  All other distros may encounter issues when running this playbook
  - **Disclaimer:** Fedora 41 is currently not compatible and may
    not work as expected
- If running this playbook locally, Ansible will need to be installed:
  - For Debian-based distros: `sudo apt install ansible-core`
  - For Fedora-based distros: `sudo dnf install ansible-core`

## Role Variables

A list of packages to be installed can be found in `defaults/main.yml`.
This list can be added to as desired, but removal of packages may cause
issues with the installation of the utilities listed above.

## Dependencies

Install the required Ansible Galaxy role and collection before running
the playbook:

```bash
ansible-galaxy install -r requirements.yml
```

## Usage

- To run locally:
  ```bash
  ansible-playbook --connection=local -i 127.0.0.1, configure_online_laptop.yml -K
  ```
- To run against a remote host:
  ```bash
  ansible-playbook -i path/to/hosts/file configure_online_laptop.yml -K --limit desired_hosts
  ```

The `-K` flag prompts for a privilege escalation password, required for package installation.

## Tags

Common packages are always installed. Use `--tags` to select which optional
utilities to install:

| Tag | Installs |
|-----|----------|
| `docker` | Docker CE |
| `vscode` | VS Code + extensions |
| `mattermost` | Mattermost Desktop |
| `yubico` | Yubico Authenticator |
| `browsers` | Chrome, Firefox, Chromium + Browserpass CE native host and extension policy |
| `1password` | 1Password app + CLI |
| `upgrade` | Upgrade all system packages |

Example — install only VS Code and Docker:
```bash
ansible-playbook --connection=local -i 127.0.0.1, configure_online_laptop.yml -K --tags=vscode,docker
```

The `upgrade` tag is opt-in and will not run unless explicitly specified.

## License

BSD-2-Clause
