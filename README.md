# Ansible Role: users_management

This role manages the creation of users and groups on a Linux system, additionally add ssh keys if desired.

## Requirements

This role requires the `ansible.posix` collection from Ansible Galaxy. To install it, run `ansible-galaxy collection install -r requirements.yml` file of module.

If the variables are empty, or if the inventory group_names is not found, this role not work by default.

## Role Variables

The configurable variables for this role include:

- `group_list`: A list of dictionaries defining the groups to be created. Each dictionary should have the `name` key and optionally the `state` key default present.
- `users_list`: A list of dictionaries defining the users to be created. Each dictionary should have the following keys:
  - `user`: The username.
  - `password`: The hashed user's password.
  - `groups`: The groups the user belongs to.
  - `shell`: The user's shell.
  - `createhome`: Whether to create the home directory, default is `true`.
  - `comment`: A comment about the user.
  - `home`: The user's home directory, default is `/home/user`.
  - `state`: The state of the user (present or absent), default is `present`.
  - `ssh_key`: The user's public SSH key.
  - `ssh_key_options`: The options to be applied to the SSH key.
  - `inventory`: Set inventory group hosts to apply changes.

## Dependencies

This role depends on the `ansible.posix` collection from Ansible Galaxy.

## Example Playbook

Here is an example of how to use this role, minimal configuration is required:

```yaml
- hosts: servers
  roles:
    - role: socket_es.users_management
      group_list:
        developers:
          name: developers
        admins:
          name: admins
      users_list:
        johndoe:
          user: johndoe
          password: "password"
          groups: developers
          shell: /bin/bash
          comment: "John Doe"
          ssh_key: "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAr..."
          ssh_key_options: 'no-port-forwarding,from="1.1.1.1"'
          inventory: test_servers
```

## License

BSD, MIT

## Author Information

This role was created in 2024 by [Juan Carlos Giménez Moncada](https://www.opensocket.es/).
