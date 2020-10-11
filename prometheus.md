# prometheus

## relabel_configs

Use relabel_configs to remove port number

```
- job_name: 'job_name'
    file_sd_configs:
      - files:
        - /etc/prometheus/targets/targets.yml
    relabel_configs:
      - source_labels: ['__address__']
        separator: ':'
        regex: '(.*):.*'
        target_label: 'instance'
        replacement: '${1}'
```

## delete series

```
$ curl -X POST -g 'http://localhost:9090/api/v1/admin/tsdb/delete_series?match[]={job="job_name"}'
$ curl -X POST http://localhost:9090/api/v1/admin/tsdb/clean_tombstones
```
