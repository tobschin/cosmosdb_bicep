# CosmosDB Example 
Creates a CosmosDb with SQL-CoreDB and a Container with pPartition Key 'id'

## Docs for Deployment

### az group deployment:
#### general:
https://learn.microsoft.com/de-de/cli/azure/group/deployment?view=azure-cli-latest

#### validate:
https://learn.microsoft.com/en-us/cli/azure/deployment/group?view=azure-cli-latest#az-deployment-group-validate

#### What if:
https://learn.microsoft.com/en-us/cli/azure/deployment/group?view=azure-cli-latest#az-deployment-group-what-if

### az bicep:
https://learn.microsoft.com/de-de/cli/azure/bicep?view=azure-cli-latest

## Do it
```sh
# list locations
az account list-locations -o table 

# set variables
RESOURCE_GROUP=rg_for_cosmosdb 
LOCATION=eastus
DEPLOYMENT_NAME=mydeployment

# create resource group
az group create --location $LOCATION --name $RESOURCE_GROUP

# validate template
az deployment group validate \
-n $DEPLOYMENT_NAME \
-g $RESOURCE_GROUP \
--template-file template.bicep \
--parameters @parameters.json 

# see what the deployment would do
az deployment group create \
-n $DEPLOYMENT_NAME \
-g $RESOURCE_GROUP \
--template-file template.bicep \
--parameters @parameters.json \
--what-if

# deploy template
az deployment group create \
-n $DEPLOYMENT_NAME \
-g $RESOURCE_GROUP \
--template-file template.bicep \
--parameters @parameters.json

# delete deployment (if you dont want to delete the whole group)
az deployment group delete -n $DEPLOYMENT_NAME -g $RESOURCE_GROUP 

# cleanup (delete resource group)
az group delete -g $RESOURCE_GROUP
```