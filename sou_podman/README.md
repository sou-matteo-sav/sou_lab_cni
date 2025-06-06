# sou_lab_cni

## Prerequisites

This role depends on the following collections (they are already available in ansible-core):

- containers.podman
- community.crypto

Also, this role is written to run with podman already installed and the podman machine running.
The role can detect if the podman machine is not running, and will tell you to start it.

## Info

This role will deploy 3 podman containers. haproxy, grafana and prometheus.
HAProxy will be exposed on port 8443, and will be used as a path-based reverse proxy.
Aftern playbook execution, grafana and prometheus can be reached calling HAProxy:
- https://localhost:8443/grafana
- https://localhost:8443/prometheus

Role will also take care of haproxy ssl certs generation.

## Usage

Playbook has a clean step that can be executed to clean the folder.

```bash
```

## Variable
Role is completely variable based, so every part can be configured in the vars folder.

## Extra Settings
In order for containers to communicate, they must be placed under the same podman network.
Their container name can be used as fqdn inside the network.

For grafana to work this setting must be set in its own conf file
root_url = %(protocol)s://%(domain)s:%(http_port)s/grafana/
serve_from_sub_path = true

For prometheus to work, this extra arg must be added in container execution
--web.external-url=/prometheus/