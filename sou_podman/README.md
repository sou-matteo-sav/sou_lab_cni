# sou_lab_cni

## Prerequisites

This role depends on the following collections (they are already available in ansible-core):

- containers.podman
- community.crypto

Also, this role has been written on a macbook twith apple M2 chip, so it needs podman already installed and the podman machine running.

The role can detect if the podman machine is not running, and will tell you to start it.

## Info

Role will deploy 3 podman containers. haproxy, grafana and prometheus.

HAProxy will be exposed on port 8443, and will be used as a path-based reverse proxy.

After playbook execution, grafana and prometheus can be reached calling HAProxy:
- https://localhost:8443/grafana
- https://localhost:8443/prometheus

Role will also take care of haproxy ssl certs generation.

## Usage

Normal execution can be achieved with the command
```bash
ansible-playbook --vault-password-file vault_pass playbook.yaml -v
```

Playbook has also a clean step that can be executed to clean the folder. It has to be invoked with an extra var that defaults to true.

```bash
ansible-playbook --vault-password-file vault_pass playbook.yaml -v --extra-vars "clean=true"
```

## Variables
Role is completely variable based, so every part can be configured in the vars file.

## Vault
Ansible vault is uploaded decrypted to improve readability, but can be encrypted with the following command

```bash
ansible-vault encrypt sou_podman/vars/main.yml
```

If you chose to encrypt vault, a vault_password file or --ask-vault-pass argument must be passed at playbook runtime.

## Extra Settings
In order for containers to communicate, they must be placed under the same podman network.
Their container name can be used as fqdn inside the network.

For grafana to work this setting must be set in its own conf file
```bash
root_url = %(protocol)s://%(domain)s:%(http_port)s/grafana/
serve_from_sub_path = true
```

For prometheus to work, this extra arg must be added in container execution
```bash
--web.external-url=/prometheus/
```

## Author

Matteo S.