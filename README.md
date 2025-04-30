<!--
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2023 Slavi Pantaleev
SPDX-FileCopyrightText: 2024 Tiz

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Loki Ansible Role

This is an [Ansible](https://www.ansible.com/) role which installs [Loki](https://grafana.com/oss/loki/) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

This role *implicitly* depends on:

- [`com.devture.ansible.role.playbook_help`](https://github.com/devture/com.devture.ansible.role.playbook_help)
- [`com.devture.ansible.role.systemd_docker_base`](https://github.com/devture/com.devture.ansible.role.systemd_docker_base)

Check [defaults/main.yml](defaults/main.yml) for the full list of supported options.

For an Ansible playbook which integrates this role and makes it easier to use, see the [mash-playbook](https://github.com/mother-of-all-self-hosting/mash-playbook).

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
