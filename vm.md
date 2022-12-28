# ARM Template

Creating resource with Azure Template and Azure CLI
```
New-AzResourceGroupDeployment
-Name mydeployment -ResourceGroupName 'psdemo-rg' `
-TemplateFile './template/template.json'
-TemplateParameterFile './template/parameters.json'
```