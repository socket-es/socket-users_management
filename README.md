# Ansible Role: users_management

This role manages the creation of users and groups on a Linux system, additionally add ssh keys if desired.

## Requirements

This role requires the `ansible.posix` collection from Ansible Galaxy. To install it, run `ansible-galaxy collection install -r requirements.yml` file of module:

## Role Variables

The configurable variables for this role include:

- `group_list`: A list of dictionaries defining the groups to be created. Each dictionary should have the `name` key and optionally the `state` key.
- `users_list`: A list of dictionaries defining the users to be created. Each dictionary should have the following keys:
  - `key`: The username.
  - `password`: The user's password.
  - `groups`: The groups the user belongs to.
  - `shell`: The user's shell.
  - `createhome`: Whether to create the home directory.
  - `comment`: A comment about the user.
  - `home`: The user's home directory.
  - `state`: The state of the user (present or absent).
  - `ssh_key`: The user's public SSH key.

## Dependencies

This role depends on the `ansible.posix` collection from Ansible Galaxy.

## Example Playbook

Here is an example of how to use this role:

```yaml
- hosts: servers
  roles:
    - role: socket_es.users_management
      group_list:
        - name: developers
          state: present
      users_list:
        - key: johndoe
          password: "password"
          groups: developers
          shell: /bin/bash
          createhome: yes
          comment: "John Doe"
          home: /home/johndoe
          state: present
          ssh_key: "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAr..."
```

## License

BSD, MIT

## Author Information

This role was created in 2024 by [Juan Carlos Giménez Moncada](https://www.opensocket.es/).
