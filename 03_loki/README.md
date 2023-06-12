# README

Demonstrates configuring loki.  

TODO

* Simple logs into loki and searching them.  

## Start

To start up Grafana

```bash
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/production/docker-compose.yaml -O docker-compose.yaml


docker compose up -d

# user:admin pwd:admin then skip
open http://localhost:3000
```


## Resources


https://grafana.com/docs/loki/latest/installation/docker/
https://grafana.com/docs/loki/latest/getting-started/