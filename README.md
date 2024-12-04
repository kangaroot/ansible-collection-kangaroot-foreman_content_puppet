# Ansible collection: kangaroot.foreman_content_puppet

Collection for configuring Puppet repositories in a Foreman/Katello installation.

The Puppet repositories that can be configured from this collection are:

Puppet 7[^1]:
- EL7
- EL8[^2]
- EL9[^2]

Puppet 8:
- EL7
- EL8[^2]
- EL9[^2]

[^1]: Enabled by default when enabling Puppet repositories.
[^2]: Enabled by default when enabling a specific Puppet version repository.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The `group_vars` directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - kangaroot.foreman_content_puppet.foreman_content_puppet
  - ...

  # OS content
  - kangaroot.foreman_content_rocky.foreman_content_rocky
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Puppet repositories are enabled and at least one of the available Puppet version and/or OS related repositories is enabled as well by setting the appropriate enable variables:

```yaml
foreman_enable_puppet: true
foreman_enable_puppet7: true
foreman_enable_puppet8: true
foreman_enable_puppet8_el8: false
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

