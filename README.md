# Ansible Role: Alertmanager for telegram

[![ubuntu-18](https://img.shields.io/badge/ubuntu-18.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![ubuntu-20](https://img.shields.io/badge/ubuntu-20.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![debian-9](https://img.shields.io/badge/debian-9.x-orange?style=flat&logo=debian)](https://www.debian.org/)
[![debian-10](https://img.shields.io/badge/debian-10.x-orange?style=flat&logo=debian)](https://www.debian.org/)
[![centos-7](https://img.shields.io/badge/centos-7.x-orange?style=flat&logo=centos)](https://www.centos.org/)
[![centos-8](https://img.shields.io/badge/centos-8.x-orange?style=flat&logo=centos)](https://www.centos.org/)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg?style=flat)](https://opensource.org/licenses/MIT)
[![GitHub issues](https://img.shields.io/github/issues/OnkelDom/ansible-role-alertmanager-telegram?style=flat)](https://github.com/OnkelDom/ansible-role-alertmanager-telegram/issues)
[![GitHub tag](https://img.shields.io/github/tag/OnkelDom/ansible-role-alertmanager-telegram.svg?style=flat)](https://github.com/OnkelDom/ansible-role-alertmanager-telegram/tags)

## Description

Deploy [telegram Alert](https://github.com/metalmatze/alertmanager-bot) using ansible.

## Requirements

- Ansible >= 2.9 (It might work on previous versions, but we cannot guarantee it)
- Community Packages: `ansible-galaxy collection install community.general`

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `proxy_env` |  {} | Set proxy environment variables |
| `telegram_version` | 1.4.1 | telegram download Version |
| `telegram_binary_install_dir` | /usr/local/bin | default bin dir |
| `telegram_config_dir` | /etc/telegram | Config Path |
| `telegram_template_dir` | "{{ telegram_config_dir }}/templates" | Template store path |
| `telegram_allow_firewall` | false | Allow access on firewalld port |
| `telegram_binary_install_dir` | /usr/local/bin | Base binary path |
| `telegram_system_user` | prometheus | User for Consul Template |
| `telegram_system_group` | prometheus | Group for Consul Template |
| `telegram_listen_port` | 2001 | telegram Alert listen Port |
| `telegram_listen_address` | 0.0.0.0 | telegram Alert listen Address |
| `telegram_config_templates` | default | default message template |
| `telegram_http_proxy` | null | set proxy to use for alert sending |
| `telegram_https_proxy` | null | set proxy to use for alert sending |
| `telegram_env_vars` | [] | custom environment vars |
| `telegram_allow_firewall` | false | allow firewall access |
| `telegram_log_level` | info | app log level |
| `telegram_alertmanager_url` | "http://127.0.0.1:9093" | alertmanager url |
| `telegram_consul_url` | "http://127.0.0.1:8500" | consul store url |
| `telegram_bolt_path` | "{{ telegram_config_dir }}/bolt.db" | database path |
| `telegram_store` | bolt | storage type |
| `telegram_telegram_token` | exmaple | telegram bot token |
| `telegram_admins` | [] | telegram admin |

## Example

### Playbook

```yaml
---
- hosts: all
  roles:
  - onkeldom.alertmanager_telegram
  vars:
    telegram_telegram_token: 2316574326510984193
    telegram_admins:
      - 148648451
      - 478984566
    alertmanager_receivers:
      - name: 'telegram'
        webhook_configs:
        - send_resolved: true
          url: http://localhost:2001
    alertmanager_child_routes:
      - receiver: "telegram"
        continue: false
        group_wait: 4h
        match_re:
          severity: "critical"
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
