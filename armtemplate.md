## ARM Template

```
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/.
    deployment Template.json#",
    "contentVersion":
    "apiProfile":
    I
    "parameters": { },
    "variables": { },
    "functions": [ ],
    "resources": [ ],
    "outputs": {}
}
```
Schema: Location of the schema location in json, that describes the json file
contentVersion: is the json version, defined by the user
apiProfile: Versioning of the resource types that are defined in the template
parameters: That are changed variables that you need in the template. Hence it can be different for prod, test and dev
variables: Are unique values that can be used again in the script
functions: Create customs function like returning a string value. You can use azure defined functions as well
resources: Are what you are planning to deploy
outputs: are output from the deployed from the resources being deployed 
