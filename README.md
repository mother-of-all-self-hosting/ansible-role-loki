# Loki Ansible Role

[loki](https://grafana.com/oss/loki/) is a log aggregation system designed to store and query logs from all your applications and infrastructure. This role helps you to set up loki:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official loki container image](https://hub.docker.com/r/grafana/loki/)


## Installing

To configure and install loki on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

## Configuration

To enable this service, add the following configuration to your `vars.yml` file and re-run the [installation](../installing.md) process:

```yaml
########################################################################
#                                                                      #
# loki                                                                 #
#                                                                      #
########################################################################

loki_enabled: true

########################################################################
#                                                                      #
# /loki                                                                #
#                                                                      #
########################################################################
```

### Exposing the web interface

By setting a hostname you will expose loki on this domain.
Usually you should also set up basic_auth in this case, otherwise everyone will be able to access your metrics

```yaml
loki_hostname: loki.example.org

# Uncommenting the following lines allows you to configure basic auth
# loki_basic_auth_enabled: true
# loki_basic_auth_username: ''
# loki_basic_auth_password: ''
```

## Usage

After [installing](../installing.md), refer to the [official documentation](https://grafana.com/docs/loki/latest/reference/api/#post-lokiapiv1push) to send logs throught loki's API withtout agent.
Promtail agent is comming soon
