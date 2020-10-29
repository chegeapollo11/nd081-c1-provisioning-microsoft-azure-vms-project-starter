# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

**Virtual Machine**
- ***Cost:*** Virtual machines are slightly more expensive with the low spec option **B1ls** averaging at **$3.8** a month but plenty of pricing options are available for selection based on client needs.
- ***Scalability:*** Scale up (cpu, memory and disk) is supported out of the box for virtual machines via azure **virtual machine scale sets**. The client would however need to implement scale out (vm instances) manually.
- ***Availability:*** This is supported out of the box via azure **availability sets**. Some work and configuration is required from the client as they have to ensure that they create at least two virtual machines then add them to an availability set.
- ***Workflow:*** A lot of the management and deployment activities have to be performed manually by the client e.g. to set up or update the application, one would have to copy the application files manually from their local machine to the virtual machine, update the application files on the virtual machine then restart the application or virtual machine for changes to take effect. Some automation can be achieved via shell scripts but these still have to be written by the client.

**App Service**
- ***Cost:*** They can be costly as well but offer a free pricing tier for dev/test purposes i.e. the **F1** pricing tier with plenty of other non free options as well.
- ***Scalability:*** Scale up (cpu, memory and disk) and scale out (vm instances) are supported out of the box for app services. Clients have the option of scaling either manually via azure portal or the command line or automatically via azure's autoscaling feature.
- ***Availability:*** This is also supported out for the box via azure **availability zones**. The client still needs to ensure that their app service environment is deployed in an availability zone.
- ***Workflow:*** Management and deployment is pretty straight forward as CI/CD solutions e.g. **Github Actions, Azure Devops Pipelines, Bitbucket Pipelines** and a few others are supported out of the box. Merging your changes to the main branch therefore automatically triggers a CI/CD pipeline that builds and deploys your latest code to azure app service while azure app service takes care of restarting your application to pick the latest changes.

**Option Selected: App Service**
The application can be accessed via this link: [Udacity Article CMS App](https://apollo-udacity-articlecms-webapp.azurewebsites.net/)

**Justification:** The main use case here was deploying a python flask application to azure and implement data storage, security and logging mainly for learning purposes. Azure app service offers a solution that fully satisfies this use case for free when using the free pricing tier hence it is cost effective.

### Assess app changes that would change your decision.

*Detail how the app and any other needs would have to change for you to change your decision in the last section.*

**For scenarios where more control over the underlying platform and the operating system is of critical essence then a virtual machine would be my option. I would also go for a virtual machine if I needed to support multiple applications and services on the same virtual machine that run on other tech stacks other than python but mainly for dev/test purposes as the free plan has a limit on the number of apps that can deployed per subscription. Currently one can deploy up to 10 apps in the free plan and resource usage quotas are also enforced daily.**