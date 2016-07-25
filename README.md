# ansible-apt-conf
* * *

## Description

Sets apt.conf entries according to a list of dictionaries, where each dictionary is an entry.

When an entry is enabled it is removed from any other file containing it and set on its path value (or default apt_conf_config_file: /etc/apt/apt.conf.d/99apt-conf-ansible-managed). If the entry is disabled it is removed from any file.

The paths where it searches for keys are /etc/apt/apt.conf and /etc/apt/apt.conf.d/*.

This role tasks are tagged with _apt-conf_ tag.

## Variables

Mandatory:
- _apt_conf_entries: dictionary of lists with entries definitions. Example:
```
apt_conf_entries:
  - key: Acquire::http::Proxy
    value: '"http://some_url";'
    enable: True
	path: /etc/apt/apt.conf.d/somefile (optional)
```

Optional:
- _apt_conf_config_file_: defaults to /etc/apt/apt.conf.d/99apt-conf-ansible-managed

## Some apt-conf entries

The 'comment' key is used below just for commenting, not used at all.

```
apt_conf_entries:
  - comment: '/etc/cron.daily/apt: upt-get update'
    key: APT::Periodic::Update-Package-Lists
    value: '"0";'
	path: /etc/apt/apt.conf.d/10periodic
    enable: True
  - comment: '/etc/cron.daily/apt: upt-get download upgradeable packages'
    key: APT::Periodic::Download-Upgradeable-Packages
    value: '"0";'
    enable: True
	path: /etc/apt/apt.conf.d/10periodic
  - key: APT::Periodic::AutocleanInterval
    value: '"0";'
    enable: True
	path: /etc/apt/apt.conf.d/10periodic
  - key: Acquire::http::Proxy
    value: '"http://host:port";'
    enable: True
	path: /etc/apt/apt.conf.d/02proxy
```
