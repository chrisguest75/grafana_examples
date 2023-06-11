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
curl -s -X GET -H "Authorization: Basic YWRtaW46YWRtaW4=" http://localhost:3000/api/datasources | yq -P --output-format=yaml 
```

## Configuring Dashboards

The example contains dashboards that were imported.  

* AWS ECS - Visualize AWS ECS metrics - ID: 551  
* AWS Billing - Visualize estimated AWS charges per AWS resource (EC2, S3, ...) - ID: 139  
* AWS SQS - Visualize AWS SQS metrics - ID: 584
* AWS SNS - Visualize AWS SNS metrics - ID: 581

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
