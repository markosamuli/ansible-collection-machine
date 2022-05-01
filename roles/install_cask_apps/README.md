# Add Homebrew cask app for installation

This is a helper role that adds applications to be installed with the
`geerlingguy.mac.homebrew` role from the [`geerlingguy.mac`][geerlingguy.mac] collection.

It checks if an application has already been installed on the system.

If the application can't be found, it adds the package name to the
`homebrew_cask_apps` variable so that the `geerlingguy.mac.homebrew` role
will then install it.

This role itself doesn't try to install any applications, but requires the
`geerlingguy.mac.homebrew` role to be called afterwards.

## Usage

```yaml
---
- hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    # This will check with "/Applications/Google Chrome.app" exists
    # and then add "google-chrome" cask to the installation list
    - name: Install Google Chrome
      import_role:
        name: install_cask_apps
      vars:
        cask_apps:
          - { name: Google Chrome }

- hosts: localhost
  connection: local
  gather_facts: false
  roles:
    - role: geerlingguy.mac.homebrew
```

[geerlingguy.mac]: https://github.com/geerlingguy/ansible-collection-mac
