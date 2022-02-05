---
layout: post
title: Установка cloud-init в ОС на linux на примере CROC cloud
---

Установка cloud-init в Rocky Linux 8.5 на примере CROC cloud

____
## Установка cloud-init для работы с облаком CROC

### Установка зависимостей

```bash
yum install -y e2fsprogs iproute net-tools procps python3-configobj python3-jinja2 python3-jsonpatch python3-jsonschema python3-libselinux python3-oauthlib python3-policycoreutils python3-PrettyTable python3-requests python3-six python3-yaml
```

### Установка пакета cloud-init

```bash
yum install cloud-init
```

### Исправляем /etc/cloud/cloud.cfg

```vim
users:
 - default

disable_root: true
preserve_hostname: false

datasource:
  Ec2:
    strict_id: false

cloud_init_modules:
 - disk_setup
 - migrator
 - bootcmd
 - write-files
 - growpart
 - resizefs
 - set_hostname
 - update_hostname
 - update_etc_hosts
 - rsyslog
 - users-groups
 - [ssh,always]

cloud_config_modules:
 - mounts
 - locale
 - set-passwords
 - rh_subscription
 - yum-add-repo
 - package-update-upgrade-install
 - timezone
 - puppet
 - chef
 - salt-minion
 - mcollective
 - disable-ec2-metadata
 - runcmd

cloud_final_modules:
 - rightscale_userdata
 - scripts-per-once
 - scripts-per-boot
 - scripts-per-instance
 - scripts-user
 - ssh-authkey-fingerprints
 - keys-to-console
 - phone-home
 - final-message
 - power-state-change

system_info:
  distro: fedora
  default_user:
    name: ec2-user
    lock_passwd: true
    gecos: CROC Cloud User
    groups: [wheel, adm, systemd-journal, adm, audio, cdrom, dialout, dip, floppy, netdev, plugdev, sudo, video]
    sudo: ["ALL=(ALL) NOPASSWD:ALL"]
    shell: /bin/bash
  paths:
    cloud_dir: /var/lib/cloud
    templates_dir: /etc/cloud/template

package_upgrade: false
package_update: true
ssh_deletekeys: false

# vim:syntax=yaml
```

## Что сделать перед тем, как передаь кому-то шаблон:

- Удалить пароль рута и поставить !! вместо этого
- Обязательно запретить логин по паролю и разрешиить по ключу
- Удалить свой ключ из authorized_keys всех пользователей.
- Очистить cloud-init