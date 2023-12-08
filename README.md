# Loki Ansible Role

*Work in progress, do NOT use yet*

[loki](https://grafana.com/oss/loki/) is a log aggregation system designed to store and query logs from all your applications and infrastructure. This role helps you to set up loki:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official loki container image](https://hub.docker.com/r/grafana/loki/)


## Installing

To configure and install loki on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

## Configuring this role for your playbook

```yaml
loki_enabled: true
loki_hostname: loki.example.org
```

## Usage



## Support

- Github issues: [mother-of-all-self-hosting/ansible-role-loki/issues](https://github.com/mother-of-all-self-hosting/ansible-role-loki.git/issues)
