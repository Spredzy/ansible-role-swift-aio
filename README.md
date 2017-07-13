# Ansible Role: Swift-AIO

Installs and configures Openstack Swift on a server.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: swift
      become: yes
      roles:
        - role: swift-aio

## Role Variables

This is the list of role variables. Examples are found below.

  * `swift_aio_bootstrap`: Bootstrap initial services (default: false)
  * `swift_aio_ks_admin_token`: Keystone Admin Token
  * `swift_aio_ks_mysql_password`: Keystone password for MySQL
  * `swift_aio_hash_prefix`: Swift hash prefix
  * `swift_aio_hash_suffix`: Swift hash suffix
  * `swift_aio_service_password`: Swift service password
  * `swift_aio_volume_device`: Device name for swift storage


## Dependencies

None.

## Example Playbook

```
- hosts: swift
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - swift-aio
```

*Inside `vars/main.yml`*:

```
---
swift_aio_ks_admin_token: changeme
swift_aio_ks_mysql_password: changeme
swift_aio_hash_prefix: changeme
swift_aio_hash_suffix: changeme
swift_aio_service_password: changeme
swift_aio_volume_device: vdb
```

## Example Run

The first time you run the playbook, set the bootstrap parameter to true.
It will bootstrap Keystone (Fernet tokens, etc...) and create the Swift ring.

```
$ ansible-playbook -i hosts playbook.yml -e swift_aio_bootstrap=true
```

After the initialization you can remove the extra variable.

```
$ ansible-playbook -i hosts playbook.yml
```

## License

Apache 2.0

## Author Information

Dimitri Savineau <dsavinea@redhat.com>



