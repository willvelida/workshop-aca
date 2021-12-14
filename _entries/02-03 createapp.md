---
sectionid: lab1-create
sectionclass: h2
title: Create an app
parent-id: lab-1
---


### Create your first app

Let's create and deploy your first hello-world application with the command `az containerapp create` which is documented [here](https://docs.microsoft.com/fr-fr/cli/azure/container). You can use a ready container image like `mcr.microsoft.com/azuredocs/containerapps-helloworld:latest`.

Don't forget to set the parameter `--ingress` to `external` to make the container app available to public requests (exposed to Internet). By adding, the query parameter, you can format the result returned by the create command: `--query configuration.ingress.fqdn`

{% collapsible %}

``` bash
az containerapp create \
  --name my-container-app \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
  --target-port 80 \
  --ingress 'external' \
  --query configuration.ingress.fqdn
```

{% endcollapsible %}

In our case, the `create` command returns (only) the container app's fully qualified domain name because we specified the `query` parameter.

![Create an with the console](/media/lab1/create-app.png)

Copy this location to a web browser to see the following message.

![Running app](/media/lab1/running-app.png)

Open the [Azure Portal](https://portal.azure.com). In your resource group, you should see your Containers apps environment but also your container app. Click on it.
From here, you can directly see, diagnose or reconfigure your application such as changing the ingress configuration, the secrets, the load balancing or the continuous deployment:

![App in Azure](/media/lab1/created-app-in-azure.png)

That's it! How simple is it to deploy and host an application! Let's start the second lab to go to a real-life usecase.

Note that you won't need these resources for the next steps of the lab. You are free to delete the resource group.