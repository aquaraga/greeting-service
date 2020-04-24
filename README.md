A Hello World REST service in SpringBoot, to be used as a scaffold to try Azure deployment using AppService compute technology

## Pre-deployment

You may create the Azure resource groups, app service plan, app service, etc. using the following Azure CLI commands:

<pre>
az login
az group create --name greeting-group --location "East US"
az appservice plan create --name greeting-plan --resource-group greeting-group --sku F1 --is-linux
az acr create --name greetingregistry --resource-group greeting-group --sku Basic --admin-enabled true
az acr repository list -n greetingregistry
az webapp create --resource-group greeting-group --plan greeting-plan --name greeting-service --deployment-container-image-name greetingregistry.azurecr.io/aquaraga/greeting
az webapp config appsettings set --resource-group greeting-group --name greeting-service --settings WEBSITES_PORT=8080
</pre>

## Debugging 

<pre>
az webapp log config --name greeting-service --resource-group greeting-group --docker-container-logging filesystem
az webapp log tail --name greeting-service --resource-group greeting-group
</pre>

