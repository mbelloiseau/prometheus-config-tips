# prometheus-config-tips

A part of my Prometheus setup

## node-exporter

By default the systemd collector returns a lot of metrics, you can reduce it by using `--collector.systemd.unit-whitelist`.

```
--collector.systemd.unit-whitelist='(ssh.service|docker.service|nginx.service|php.+fpm.service)'
``` 

Example on a basic web server

```
# without collector.systemd.unit-whitelist
$ curl -s localhost:9100/metrics | grep -c ^node_systemd_unit_state
870
# with collector.systemd.unit-whitelist
$ curl -s localhost:9100/metrics | grep -c ^node_systemd_unit_state
20
```
