# App service

## App service isolated vs not isolated

## Non isolated App service plans

Not isolated App service plans are:
- F1 and D1 Free and Shared --> Run on shared infrastructure 
- B1, B2, B3 Basic type --> Lower traffic requirements, for development and testing, don't need advance autoscaling, Not for production
- S1, S2, S3 Standard type --> For Production, Price is based on number of instances you run, autoscaling, 
- P1v2, P2v2, P3v2 Premium v2 --> Designed to provide enhanced performance,
- P1v3, P2v3, P3v3 Premium v3 --> Upgraded premium plan

## Isolated App service environment (ASE)

- Fully isolated and dedicated environment for running webapps
- High scale and high utilization
- Isolation and secure network access
- Fine grain control over network traffic --> Network security group
- Apps on Vent can connect over VPM to on premises resources

![Alt text](./Pictures/appservice/isolated_app_service.png?raw=true "Title")

![Alt text](./Pictures/appservice/isolated_app_service_2.png?raw=true "Title")

## az cli deployment

```
az group create -n webapps-dev-rg -1 westus2

az appservice plan create --name webapps-dev-plan \
    --resource-group webapps-dev-rg \
    --sku s1 \
    --is-linux

az webapp create -g webapps-dev-rg \
    -p webapps-dev-plan \
    -n mp10344884 \
    --runtime "node | 10.14"

```

## az shell

```
# Create variables
$webappname "mywebapp$(Get-Random)" I
$rgname 'webapps3-dev-rg'
$location = 'westus2'

## Create a resource group
New-AzResourceGroup -Name $rgname -Location $location

## Create an App Service plan in S1 tier
New-AzAppServicePlan -Name $webappname -Location $location ResourceGroupName $rgname -Tier S1

New-AzWebApp -Name $webappname -Location $location -AppServicePlan $webappname -ResourceGroupName $rgname


## Create with resource template

To create it you need to create the resource and then use azure resource group deployment with template URL

```
New-AzResourceGroup -Name <resource-group-name> -Location <resource-group-location> #use this command when you need to create a new resource group for your deployment
New-AzResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-webapp-ba...
```

```
az group create --name I resource-group-name> --location <resource-group-location> #use this command when you need to create a new resource group for your deployment
az group deployment create --resource-group <my-resource-group> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-webapp-basic-1:...
```


```