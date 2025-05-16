<!--
SPDX-FileCopyrightText: 2020 - 2024 MDAD project contributors
SPDX-FileCopyrightText: 2020 - 2024 Slavi Pantaleev
SPDX-FileCopyrightText: 2020 Aaron Raimist
SPDX-FileCopyrightText: 2020 Chris van Dijk
SPDX-FileCopyrightText: 2020 Dominik Zajac
SPDX-FileCopyrightText: 2020 Mickaël Cornière
SPDX-FileCopyrightText: 2022 François Darveau
SPDX-FileCopyrightText: 2022 Julian Foad
SPDX-FileCopyrightText: 2022 Warren Bailey
SPDX-FileCopyrightText: 2023 Antonis Christofides
SPDX-FileCopyrightText: 2023 Felix Stupp
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2023 Pierre 'McFly' Marty
SPDX-FileCopyrightText: 2024 Tiz
SPDX-FileCopyrightText: 2024 - 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Setting up Loki

This is an [Ansible](https://www.ansible.com/) role which installs [Loki](https://grafana.com/oss/loki/) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

Loki is a log aggregation system designed to store and query logs from all your applications and infrastructure.

See the project's [documentation](https://grafana.com/docs/loki/latest/) to learn what Loki does and why it might be useful to you.

## Prerequisites

As Loki is just a log storage system, you would need at least two other components in order to make use of it:

- an agent such as [Promtail](https://grafana.com/oss/promtail/) to send logs to Loki
- a system such as [Grafana](https://grafana.com/) to read the logs out of Loki and display them nicely

If you are looking for Ansible roles for them, you can check out [ansible-role-promtail](https://github.com/mother-of-all-self-hosting/ansible-role-promtail) and [ansible-role-grafana](https://github.com/mother-of-all-self-hosting/ansible-role-grafana), both of which are maintained by the [Mother-of-All-Self-Hosting (MASH)](https://github.com/mother-of-all-self-hosting) team.

## Adjusting the playbook configuration

To enable Loki with this role, add the following configuration to your `vars.yml` file.

**Note**: the path should be something like `inventory/host_vars/mash.example.com/vars.yml` if you use the [MASH Ansible playbook](https://github.com/mother-of-all-self-hosting/mash-playbook).

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

### Set the hostname to expose the web interface (optional)

You may wish to expose Loki's web interface, if you'd like to be able to:

- push logs from remote agents (e.g. Promtail installed on remote machines, etc.)
- query logs from remote systems (e.g. Grafana installed elsewhere)

You can expose the interface by setting the hostname on your `vars.yml` file as below:

```yaml
loki_hostname: example.com
```

Make sure to replace `example.com` with your own value.

After adjusting the hostname, make sure to adjust your DNS records to point the domain to your server.

#### Set up Basic Authentication

When exposing metrics publicly, you might also probably want to set up [HTTP Basic Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) **or anyone would be able to read your logs or push new ones**.


To set up the authentication, add the following configuration to your `vars.yml` file.

```yaml
loki_container_labels_metrics_middleware_basic_auth_enabled: true

loki_container_labels_metrics_middleware_basic_auth_users : 'USERNAME_HERE:HASHED_PASSWORD_HERE'
```

Make sure to replace `USERNAME_HERE` and `HASHED_PASSWORD_HERE` with your own values.

You can create users by running `htpasswd -nb USERNAME_HERE PASSSWORD_HERE`.

### Extending the configuration

There are some additional things you may wish to configure about the component.

Take a look at:

- [`defaults/main.yml`](../defaults/main.yml) for some variables that you can customize via your `vars.yml` file. You can override settings (even those that don't have dedicated playbook variables) using the `loki_environment_variables_additional_variables` variable

## Usage

Refer to the [official documentation](https://grafana.com/docs/loki/latest/reference/api/#post-lokiapiv1push) for details about how to send logs throught Loki's API without an agent.

## Troubleshooting

### Check the service's logs

You can find the logs in [systemd-journald](https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html) by logging in to the server with SSH and running `journalctl -fu loki` (or how you/your playbook named the service, e.g. `mash-loki`).
