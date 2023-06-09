# README

Demonstrates configure a basic Grafana dashboard

## Start

To start up Grafana

```bash
docker compose up -d

# user:admin pwd:admin then skip
open http://localhost:3000
```

```sh
# Check scrape configuration 
open http://localhost:9090
```

## Configuring Data Sources

We can manually add a datasource or we can use the automated provisioning system. [Docs](https://grafana.com/docs/grafana/latest/administration/provisioning/)

Once created you can export it as json.  

```sh
curl -X GET -H "Authorization: Basic YWRtaW46YWRtaW4=" http://localhost:3000/api/datasources
```

## Troubleshooting

To exec into the grafana container.

```sh
docker compose exec -it grafana /bin/bash  
```

## Resources

* GrafanaLabs [here](https://grafana.com/)  
