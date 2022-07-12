# Monitoring-on-confluent-cloud

The main objective of this project is to provide key steps to configure Prometheus to scarify metrics from the Confleunt cloud API metric endpoint and work as a data source for Grafana which is a dashboard creation and visualization tool. 
![image](https://user-images.githubusercontent.com/103249046/178447755-ba18bcb5-6818-45f2-ae46-bea2cd863cb6.png)

## Requirements:
-A Confluent account cloud and organization 
-Confluent cli 
-Docker 

## Steps : 

### Step1: Create  Cluster API KEY 

First , lets strat by creating  a service account and give it the role of a Metrics Viewer either by creating it manually on coufluent cloud or by y using the following cli command. 
1-Login into confluent cloud account , this step requieres the confluent cloud account username and password .

```bash
$confluent login --save
```
2-Create the service account ( the descriptor fieled is optionnal).

```bash
$confluent iam service-account create MetricsImporter --description "A  service account to import Confluent Cloud metrics into Prometheus"
```
3-Add the MetricsViewer role to the service account, replace the $sa-id by your service account ID ( looks like  sa-d91gmd)

```bash
$confluent iam rbac role-binding create --role MetricsViewer --principal User:$sa-id
```

Now , let's assign an api key to our Metrics viewer service account . The cluster API Key gives us acces to retrieve metrics from the confluent cloud API metrics . You can create it directly on confluent cloud manualy or by using the following cli command . 

```bash
$confluent api-key create --resource cloud --service-account $sa-id
```
