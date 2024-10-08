
# App Service

## App Service Environment
                
### Create resource group, Virtual Network and App Service Environment v3 with default values.
az group create -g MyResourceGroup --location westeurope

az network vnet create -g MyResourceGroup -n MyVirtualNetwork --address-prefixes 10.0.0.0/16 --subnet-name MyAseSubnet --subnet-prefixes 10.0.0.0/24

az appservice ase create -n MyAseName -g MyResourceGroup --vnet-name MyVirtualNetwork --subnet MyAseSubnet --kind asev3

### List app service environments.
az appservice ase list [--resource-group]

### Show details of an app service environment.
az appservice ase show --name
                       [--resource-group]

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

## Webapp deployment

az webapp deployment source config --repo-url
                                   [--branch]
                                   [--git-token]
                                   [--github-action]
                                   [--ids]
                                   [--manual-integration]
                                   [--name]
                                   [--repository-type {externalgit, git, github, localgit, mercurial}]
                                   [--resource-group]
                                   [--slot]
                                   [--subscription]
                                   
### Manage deployment from git or Mercurial repositories
az webapp deployment source config --branch master --manual-integration --name MyWebApp --repo-url https://github.com/Azure-Samples/function-image-upload-resize --resource-group MyResourceGroup

### Deployment by using zip file content
az webapp deployment source config-zip -g {myRG} -n {myAppName} --src {zipFilePathLocation}

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

## Webapp connection

### Connection create app-insights
az webapp connection create app-insights

### Create a connection between webapp and appconfig
az webapp connection create appconfig

### Create a connection between webapp and keyvault 
az webapp connection create keyvault

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

### Webapp scale
az webapp scale -g MyResourceGroup -n MyApp --instance-count 2
