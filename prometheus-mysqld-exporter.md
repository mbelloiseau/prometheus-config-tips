# prometheus-mysqld-exporter

Create a dedicated user for mysqld exporter

```sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY '<your strong password>';
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'localhost';
FLUSH PRIVILEGES;
```

* /etc/default/prometheus-mysqld-exporter

```
ARGS='-config.my-cnf /var/lib/prometheus/my.cnf'
```

* /var/lib/prometheus/my.cnf

```
[client]
host		= localhost
user		= exporter
password	= <your strong password>
```

Check your config `service prometheus-mysqld-exporter restart` and `curl -s localhost:9104/metrics`
