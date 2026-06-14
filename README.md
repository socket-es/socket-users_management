# Ansible Role: users_management

This role manages the creation of users and groups on a Linux system, additionally add ssh keys if desired.

## Requirements

This role requires the `ansible.posix` collection from Ansible Galaxy. To install it, run `ansible-galaxy collection install -r requirements.yml` file of module.

If the variables are empty, or if the inventory group_names is not found, this role not work by default.

## Role Variables

The configurable variables for this role include:

- `groups_list`: A list of dictionaries defining the groups to be created. Each dictionary should have the following keys:
  - `name`: Name of the group on system.
  - `state`: The state of the group (present or absent), default is `present`.
  - `sudo`: Allow sudo to group on system with full permissions, default is `false`.
  - `inventory`: Set inventory group hosts to apply changes. Defaults to "all". Multiple inventories can be comma-separated.
- `users_list`: A list of dictionaries defining the users to be created. Each dictionary should have the following keys:
  - `user`: The username.
  - `password`: The hashed user's password.
  - `uid`: Optionally sets the UID of the user.
  - `expires`: An expiry time for the user in epoch (example 1422403387).
  - `groups`: The groups the user belongs to. And the principal group for home folder is the first group in the groups list.
  - `chmod`: Set custom chmod for user home, default is `700`.
  - `shell`: The user's shell.
  - `createhome`: Whether to create the home directory, default is `true`.
  - `comment`: A comment about the user.
  - `home`: The user's home directory, default is `/home/user`.
  - `state`: The state of the user (present or absent), default is `present`.
  - `ssh_key`: The user's public SSH key, this is optional.
  - `ssh_key_options`: The options to be applied to the SSH key, this is optional.
  - `inventory`: Set inventory group hosts to apply changes. Defaults to "all". Multiple inventories can be separated by commas (e.g., "web,db"). Note: If a host does not belong to the specified inventory, the user and their home directory will be aggressively removed from the system (Zero-Trust policy).

## Dependencies

This role depends on the `ansible.posix` collection from Ansible Galaxy.

## Example Playbook

Here is an example of how to use this role, minimal configuration is required:

```yaml
- hosts: servers
  roles:
    - role: socket_es.users_management
      groups_list:
        developers:
          name: developers
          sudo: true
          inventory: "webservers,dbservers"
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
          inventory: "test_servers,production_servers"
```

## License

BSD, MIT

## Author Information

This role was created in 2024 by [Juan Carlos Giménez Moncada](https://www.opensocket.es/).

