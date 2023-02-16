# Azure Functions

## Defination:

Serverless: Rather than maintaining servers ourselves, we delegate it to 
- Automated scaling up
- Pay as you go model

Choices for plans:

- Consumption Plan: 
    - Serverless
    - Automated Scale
    - TimesOut im 5 mins

- App Service Plan
    - Traditional pricing model -- Pay monthly
    - No restrictions

- Premium Plan
    - Speed
    - Enhanced Security 
    - Reserved Instances
    - Automatic scaling capabilities

- Docker Container
    - Can run on any premises
    - In any cloud

- Function.json file defines all the triggers and bindings used by an azure function

### Trigger
ONLY one trigger for a function
- HTTP trigger - use for API and webhooks
    - Any HTTP method
    - Route 
    - Can be secured via authorization key. There are three levels
        - Anonymous: no key required
        - Function: key per function
        - Admin: key per app (one key for all the functions in the app)
- Time trigger - use for schedule tasks
- Queue trigger - run in response to a message on a queue
	- you need to specify the path of the blob too with a binding expression
```
sample-workingItem/{name}
```
		- {name} will allow the function to access the file that triggered the function
		- 
- Cosmos DB trigger - runs when a document is created or updated
- Blob Trigger - run when a new file is uploaded to Blob Storage
- Event Grid
- Microsoft Graph


### Binding

All the inbound and outbound binding is stored in function.json for all the functions

- Input binding examples like: bobstorage, cosmos db binding, and microsoft graph binding
- Output binding examples: blobstorage, queue storage, cosmos dd, eventhub, servicehub, sendgrid 

