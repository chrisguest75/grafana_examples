# README

Demonstrates configuring grafana with AWS cloudwatch datasource  

TODO:

* costs
* cloudwatch

## Start

To start up Grafana

```bash
cd 02_aws_grafana

# show the role
cat ~/.aws/credentials  
# create the datasources
mkdir -p provisioning/datasources
yq e '(.datasources[].jsonData["assumeRoleArn"]) |= "arn:aws:iam::000000000000:role/myrole"' ./provisioning/datasources.template/cloudwatch.yaml > ./provisioning/datasources/cloudwatch.yaml

docker compose up -d

# user:admin pwd:admin then skip
open http://localhost:3000
```

## Configuring Data Sources

We can manually add a datasource or we can use the automated provisioning system. [Docs](https://grafana.com/docs/grafana/latest/administration/provisioning/)  

Once created you can export it as json.  

```sh
curl -X GET -H "Authorization: Basic YWRtaW46YWRtaW4=" http://localhost:3000/api/datasources
```

## Cleanup

```bash
docker compose down
```

## Troubleshooting

To exec into the grafana container.

```sh
# To exec into the grafana container.  
docker compose exec -it grafana /bin/bash  
# aws credentials are shared into .aws.  
ls -la

# get logs 
docker compose logs grafana
```

## Resources

* GrafanaLabs [here](https://grafana.com/)  
* Provision dashboards and data sources [here](https://grafana.com/tutorials/provision-dashboards-and-data-sources/)  
* Provision Grafana [here](https://grafana.com/docs/grafana/latest/administration/provisioning/#datasources)  
