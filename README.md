# ansible-apt-conf
* * *

## Description

Sets apt.conf entries according to a list of dictionaries, where each dictionary is an entry.

When an entry is enabled it is removed from any other file containing it and set on {{ apt_conf_config_file }} file (by default /etc/apt/apt.conf.d/99apt-conf-ansible-managed. If the entry is disabled it is removed from any file including {{ apt_conf_config_file }}.

This role tasks are tagged with _apt-conf_ tag.

## Variables

Mandatory:
- _apt_conf_entries: dictionary of lists with entries definitions. Example:
```
apt_conf_entries:
  - key: Acquire::http::Proxy
    value: '"http://some_url";'
    enable: True
```

Optional:
- _apt_conf_config_file_: defaults to /etc/apt/apt.conf.d/99apt-conf-ansible-managed

## Some apt-conf entries

apt_conf_entries:
  - comment: /etc/cron.daily/apt: upt-get update
    key: APT::Periodic::Update-Package-Lists
    value: '"0";'
    enable: True
  - comment: /etc/cron.daily/apt: upt-get download upgradeable packages
    key: APT::Periodic::Download-Upgradeable-Packages
    value: '"0";'
    enable: True
  - key: APT::Periodic::AutocleanInterval
    value: '"0";'
    enable: True
