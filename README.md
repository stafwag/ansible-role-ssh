# Ansible Role: ssh

An ansible role to manage sshd/ssh

# Installation

## Ansible galaxy

The role is available on [Ansible Galaxy](https://galaxy.ansible.com/stafwag/ssh).

To install the role from Ansible Galaxy execute the command below.

```bash
ansible-galaxy install stafwag.ssh
```

## Source Code

If you want to use the source code directly.

Clone the role source code.

```bash
$ git clone https://github.com/stafwag/ansible-role-ssh/ stafwag.ssh
```

and put into the [role search path](https://docs.ansible.com/ansible/2.4/playbooks_reuse_roles.html#role-search-path)

## Requirements

ssh

## Role Variables

### Playbook related variables

* **ssh**:
  "namespace"
  * **sshd_config**:
    * **linesinfile**:  Array of lineinfile
      * **regexp**: The regular expression to look for in every line of the file.
      * **state**: absent | present (default)
      * **line**:  The line to insert/replace into the file.
      * **backrefs**: no (default) | yes


## Dependencies

None

## Example Playbook

```
- name: Configure sshd
  hosts: all
  become: true
  roles:
    - role: stafwag.ssh
      vars:
        ssh:
          sshd_config:
            linesinfile:
            - name:   set MaxAuthTries
              regex:  '^#*MaxAuthTries'
              line:   'MaxAuthTries 12'
            - name:    disable password authentication
              regexp: '^#*PasswordAuthentication'
              line:   'PasswordAuthentication no'
            - name:   remove password authentication
              regexp: '(?i)^\s*PasswordAuthentication\s*yes.*'
              state:  absent
            - name:   disable root acesss
              regexp: '^#*PermitRootLogin'
              line:   'PermitRootLogin no'
            - name:   remove root acesss
              regexp: '(?i)^\s*PermitRootLogin\s*yes'
              state:  absent
```


## License

MIT/BSD

## Author Information

Created by Staf Wagemakers, Email: staf@wagemakers.be, Website: [https://www.wagemakers.be](https://www.wagemakers.be), My company: [https://mask27.dev](https://mask27.dev)
