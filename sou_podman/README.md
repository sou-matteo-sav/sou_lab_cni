# sou_lab_cni
=========

## Info

This role will deploy 3 podman containers. haproxy, grafana and prometheus.
It will take care of haproxy ssl certs generation.

## Warning

For grafana to work this setting must be set in its own conf file
serve_from_sub_path = true