# Azure CLI

```
az acr create \
--resource-group psdemo-rg \
--name $ACR_NAME \
--sku Standard
```

## Getting the domain url for ACR

```
ACR_LOGINSERVER=$(az acr show --name $ACR_NAME --query loginServer --output tsv)
```

## Pushing an Image into ACR need to tag local build with full domain url for acr
```
docker tag webappimage:v1 $ACR_LOGINSERVER/webappimage:v1
docker push $ACR_LOGINSERVER/webappimage:v1
```

## Build using ACR Tasks
All of it could be done in one line:
This requires to be run in the same dir as dockerfile so it can build the image from it directly and we wouldn't need to use docker tag and docker push
```
az acr build --image "webappimage:v1-acr-task" --registry $ACR_NAME .
```

## See acr images that are pushed

```
az acr repository show-tags --name $ACR_NAME --repository webappimage --output table
```
## Creating SP

Note: Remember you need to define sp to pull or push images to ACR

```
az ad sp create-for-rbac
    --name http://$ACR_NAME-pull \
    --scopes $ACR_REGISTRY_ID \
    --role acrpull

```

In order for us to store the password we can use flag called --query and output it as tsv


```
ACR_NAME='psdemoacr'
ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)
SP_NAME=acr-service-principal
SP_PASSWD=$(az ad sp create-for-rbac \
    --name http://$ACR_NAME-pull \
    --scopes $ACR_REGISTRY_ID \
    --role acrpull \
    --query password \
    --output tsv)
```

We can get the SP APPID with ``` az ad sp show  --id ... ``` 

```
SP_APPID=$(az ad sp show \
    --id http://$ACR_NAME-pull \
    --query appId \
    --output tsv)
```

APPID is used as a username when authenticating sp to pull or push the image to ACR

## Running and creating a container in ACI from ACR

- We first get the server url for ACR for the domain url for image
- To create a container we use ``` az container create ``` and pass in resource group of the ACI, the name of the container
- Most importantly we need to pass ``` --dns-name-label ``` that will be the access domain name for the container
- It requires the port number with ``` --port ``` that the application will be listening on
-  ``` --image $ACR_LOGINSERVER/webappimage:v1 ``` We need to define the domain of the server url and the image name with the tag we want to deploy to the ACI container
- For ACI to authenticate itself to ACR, it needs these flags (you only need it for private registries like ACR):
    - ```--registry-login-server $ACR_LOGINSERVER ``` defining the ACR's login server url
    - ``` --registry-username $SP_APPID ``` Defining the SP APPID as userID to authenticate the ACI to pull from ACR with SP
    - ``` --registry-password $SP_PASSWD ``` same needs to be done for the password for SP to authenticate ACI to pull image from ACR with SP

The full code is here:

```
ACR_LOGINSERVER=$(az acr show --name $ACR_NAME --query loginServer --output tsv)
az container create l
--resource-group psdemo-rg \
--name psdemo-webapp-cli \
--dns-name-label psdemo-webapp-cli \
--ports 80 \
--image $ACR_LOGINSERVER/webappimage:v1 \
--registry-login-server $ACR_LOGINSERVER \
--registry-username $SP_APPID \
--registry-password $SP_PASSWD
```

## Look at the aci running

```
az container show --resource-group someRG --name someName
```

## To see the container logs

```
az container logs --resource-group someRG --name someName
```