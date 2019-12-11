# Ansible Role: ssh

An ansible role to manage sshd/ssh

## Requirements

None

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
- name: configure sshd
  hosts: all
  become: true
  vars:
    ssh:
        sshd_config:
          linesinfile:
          - name:   set MaxAuthTries
            regex:  '^#*MaxAuthTries'
            line:   'MaxAuthTries 12'
          - name:   remove password authentication
            regexp: '^#*PasswordAuthentication'
            line:   'PasswordAuthentication no'
          - name:   remove root acesss
            regexp: '^#*PermitRootLogin'
            line:   'PermitRootLogin no'
  roles:
    - stafwag.ssh
```


## License

MIT/BSD

## Author Information

Created by Staf Wagemakers, email: staf@wagemakers.be, website: http://www.wagemakers.be.
