<!--
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2024 Tiz

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Loki Ansible Role

[Loki](https://grafana.com/oss/loki/) is a log aggregation system designed to store and query logs from all your applications and infrastructure. This role helps you to set up Loki:

- with everything run in [Docker](https://www.docker.com/) containers
- powered by [the official Loki container image](https://hub.docker.com/r/grafana/loki/)


## Installing

To configure and install Loki on your own server(s), you should use a playbook like [Mother of all self-hosting](https://github.com/mother-of-all-self-hosting/mash-playbook) or write your own.

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

By setting a hostname you will expose Loki on this domain.
Usually you should also set up basic_auth in this case, otherwise everyone will be able to access your metrics

```yaml
loki_hostname: loki.example.org

# Uncomment following lines to add basic auth
#loki_container_labels_metrics_middleware_basic_auth_enabled: true
#loki_container_labels_metrics_middleware_basic_auth_users : '<user>:<hashed_password>'

```

## Usage

After [installing](../installing.md), refer to the [official documentation](https://grafana.com/docs/loki/latest/reference/api/#post-lokiapiv1push) to send logs throught loki's API without an agent.
The [Promtail agent](https://grafana.com/docs/loki/latest/send-data/promtail/) is coming soon
