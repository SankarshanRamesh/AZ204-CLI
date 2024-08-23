
# App Service

### App Service Environment
az appservice ase create --name
                         --resource-group
                         --subnet
                         [--force-network-security-group {false, true}]
                         [--force-route-table {false, true}]
                         [--front-end-scale-factor]
                         [--front-end-sku {I1, I2, I3}]
                         [--ignore-network-security-group {false, true}]
                         [--ignore-route-table {false, true}]
                         [--ignore-subnet-size-validation {false, true}]
                         [--kind {ASEv2, ASEv3}]
                         [--location]
                         [--no-wait]
                         [--os-preference {Linux, Windows}]
                         [--virtual-ip-type {External, Internal}]
                         [--vnet-name]
                         [--zone-redundant {false, true}]


### Create resource group, Virtual Network and App Service Environment v3 with default values.
az group create -g MyResourceGroup --location westeurope

az network vnet create -g MyResourceGroup -n MyVirtualNetwork --address-prefixes 10.0.0.0/16 --subnet-name MyAseSubnet --subnet-prefixes 10.0.0.0/24

az appservice ase create -n MyAseName -g MyResourceGroup --vnet-name MyVirtualNetwork --subnet MyAseSubnet --kind asev3

### List app service environments.
az appservice ase list [--resource-group]

### Show details of an app service environment.
az appservice ase show --name
                       [--resource-group]

### Create an app service plan.
az appservice plan create --name
                          --resource-group
                          [--app-service-environment]
                          [--hyper-v]
                          [--is-linux]
                          [--location]
                          [--no-wait]
                          [--number-of-workers]
                          [--per-site-scaling]
                          [--sku {B1, B2, B3, D1, F1, FREE, I1, I1MV2, I1V2, I2, I2MV2, I2V2, I3, I3MV2, I3V2, I4MV2, I4V2, I5MV2, I5V2, I6V2, P0V3, P1MV3, P1V2, P1V3, P2MV3, P2V2, P2V3, P3MV3, P3V2, P3V3, P4MV3, P5MV3, S1, S2, S3, SHARED, WS1, WS2, WS3}]
                          [--tags]
                          [--zone-redundant]

### Create a basic app service plan.
az appservice plan create -g MyResourceGroup -n MyPlan

### Create a standard app service plan with four Linux workers.
az appservice plan create -g MyResourceGroup -n MyPlan --is-linux --number-of-workers 4 --sku S1

### Create a Windows container app service plan.
az appservice plan create -g MyResourceGroup -n MyPlan --hyper-v --sku P1V3

### Create an app service plan for app service environment.
az appservice plan create -g MyResourceGroup -n MyPlan --app-service-environment MyAppServiceEnvironment --sku I1

### Delete an app service plan.
az appservice plan delete [--ids]
                          [--name]
                          [--resource-group]
                          [--subscription]
                          [--yes]
### List app service plans.
az appservice plan list [--resource-group]

### Get the app service plans for a resource group or a set of resource groups.
az appservice plan show [--ids]
                        [--name]
                        [--resource-group]
                        [--subscription]

# Webapp

### Open a web app in a browser
az webapp browse [--ids]
                 [--logs]
                 [--name]
                 [--resource-group]
                 [--slot]
                 [--subscription]

### Create a web app.
az webapp create --name
                 --plan
                 --resource-group
                 [--acr-identity]
                 [--acr-use-identity]
                 [--assign-identity]
                 [--basic-auth {Disabled, Enabled}]
                 [--container-image-name]
                 [--container-registry-password]
                 [--container-registry-url]
                 [--container-registry-user]
                 [--deployment-container-image-name]
                 [--deployment-local-git]
                 [--deployment-source-branch]
                 [--deployment-source-url]
                 [--docker-registry-server-password]
                 [--docker-registry-server-user]
                 [--https-only {false, true}]
                 [--multicontainer-config-file]
                 [--multicontainer-config-type {COMPOSE, KUBE}]
                 [--public-network-access {Disabled, Enabled}]
                 [--role]
                 [--runtime]
                 [--scope]
                 [--startup-file]
                 [--subnet]
                 [--tags]
                 [--vnet]

### Create a web app with the default configuration.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName

### Create a web app with a NodeJS 10.14 runtime and deployed from a local git repository.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName --runtime "node:12LTS" --deployment-local-git

### Create a web app with a Java 11 runtime.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName --runtime "java:11:Java SE:11"

### Create a web app with an image from DockerHub.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName -i nginx

### Create a web app with an image from a private DockerHub registry.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName -i MyImageName -s username -w password

### Create a web app with an image from a private Azure Container Registry.
az webapp create -g MyResourceGroup -p MyPlan -n MyUniqueAppName -i myregistry.azurecr.io/docker-image:tag

### Delete a web app.
az webapp delete [--ids]
                 [--keep-dns-registration]
                 [--keep-empty-plan]
                 [--keep-metrics]
                 [--name]
                 [--resource-group]
                 [--slot]
                 [--subscription]

### Deploy a static text file to wwwroot/staticfiles/test.txt
az webapp deploy --resource-group ResourceGroup --name AppName --src-path SourcePath --type static --target-path staticfiles/test.txt

### Restart a web app.
az webapp restart [--ids]
                  [--name]
                  [--resource-group]
                  [--slot]
                  [--subscription]

### Set a web app's settings.
az webapp config appsettings set [--ids]
                                 [--name]
                                 [--resource-group]
                                 [--settings]
                                 [--slot]
                                 [--slot-settings]
                                 [--subscription]
### Delete web app settings.
az webapp config appsettings delete --setting-names
                                    [--ids]
                                    [--name]
                                    [--resource-group]
                                    [--slot]
                                    [--subscription]

### Webapp config connection-string set
az webapp config connection-string set [--connection-string-type {ApiHub, Custom, DocDb, EventHub, MySql, NotificationHub, PostgreSQL, RedisCache, SQLAzure, SQLServer, ServiceBus}]
                                       [--ids]
                                       [--name]
                                       [--resource-group]
                                       [--settings]
                                       [--slot]
                                       [--slot-settings]
                                       [--subscription]

### Add a mysql connection string.
az webapp config connection-string set -g MyResourceGroup -n MyUniqueApp -t mysql --settings mysql1='Server=myServer;Database=myDB;Uid=myUser;Pwd=myPwd;'

## Webapp deployment slot

### Swap a staging slot into production
az webapp deployment slot swap  -g MyResourceGroup -n MyUniqueApp --slot staging --target-slot production

### Deployment slot create
az webapp deployment slot create --name MyWebapp --resource-group MyResourceGroup --slot staging

### Deployment slot delete
az webapp deployment slot delete --name MyWebapp --resource-group MyResourceGroup --slot staging

## Webapp log config

### Configure logging for a web app
az webapp log config [--application-logging {azureblobstorage, filesystem, off}]
                     [--detailed-error-messages {false, true}]
                     [--docker-container-logging {filesystem, off}]
                     [--failed-request-tracing {false, true}]
                     [--ids]
                     [--level {error, information, verbose, warning}]
                     [--name]
                     [--resource-group]
                     [--slot]
                     [--subscription]
                     [--web-server-logging {filesystem, off}]

### Configure logging for a web app
az webapp log config --name MyWebapp --resource-group MyResourceGroup --web-server-logging off
