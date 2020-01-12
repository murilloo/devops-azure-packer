# devops-aws-packer-pipeline
Example pipeline using Packer to create a server image on top of Azure with customized configuration

## Requirements
- Azure CLI >= 2.0.78 (https://docs.microsoft.com/en-us/cli/azure)
- Packer >= 1.5.1 (https://packer.io/downloads.html)
- Python version = 3.7.5
- Ansible = 2.9.2

## Create Azure resource group
```
az group create -n devops-azure-packer-pipeline -l eastus
```

## Create Azure credentials
```
az ad sp create-for-rbac --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"
az account show --query "{ subscription_id: id }"
```

## Variables
Export the variables below to your runtime *before* executing *packer*
```
AZURE_CLIENT_ID="xxxxxxxxx"
AZURE_CLIENT_SECRET="xxxxxxxxx"
AZURE_TENANT_ID="xxxxxxxxx"
AZURE_SUBSCRIPTION_ID="xxxxxxxxx"
```

## Goals
- To bootstrap a server image running Ubuntu 16.04 LTS
- To install Nginx on top of it
- To publish it to Azure

## Running
```
$ packer validate template.json
$ packer build template.json
```
