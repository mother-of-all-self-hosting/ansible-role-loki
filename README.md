# loki Ansible Role

[loki](https://www.influxdata.com/) is a self-hosted time-series database. This role helps you to set up loki:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official loki container image](https://hub.docker.com/r/_/loki/)

## Prerequisits

* A installed and running [infuxdb](https://www.influxdata.com/).


## Installing

To configure and install loki on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

## Configuring this role for your playbook

This role depends on a influxdb configuring loki. You need to obtain the influx token and config link in the influxdb.
In your browser, visit the influxdb and go to Load Data -> loki.
There you need to add a loki configuraion. You can now obtain these values from the setup instructions and oaste them here.

```yaml
loki_enabled: true
loki_influx_token: SUPERSECRETTOKEN
loki_config_link: https://influxdb.example.org/api/v2/lokis/01234569
```

## Usage

In your influxdb configure the loki plugins as you like.

## Support

- Github issues: [mother-of-all-self-hosting/ansible-role-loki/issues](https://github.com/mother-of-all-self-hosting/ansible-role-loki.git/issues)
