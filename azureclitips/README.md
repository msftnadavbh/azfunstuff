# Azure CLI Tips & Tricks

## Intro

Overall, most people are aware of the basics of Azure CLI.

e.g listing VMs, getting the running state of a particular resource, etc.

In this article, I'll give you some great tips on enhancing your work with Azure CLI,

Leveraging its power over basically any other way of interacting with Azure.

If you haven't already installed Azure CLI, [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) it is.

## Make Azure CLI Yours
After you've installed Azure CLI, set your default account using __az login__ :

` az login `

Then, lookup your most used subscription ID and set it as default using :

` az account set -s $subid `

Now, on to the fun stuff.

Run __az configure__ to get Azure CLI's current settings, we'll tweak them a bit :

` az configure `

You'll the below output :

![az configure](/azureclitips/images/1.png)

Let's run through the stuff here.

__Cloud Name__ basically means the current Azure Cloud that you're using. This is doesn't need to be changed unless you're using Azure Gov.

__defaults__ needs some more elaboration. As you can see, my default location is set to East US. This means if I dont set the -l trigger at resource creation,
Azure CLI will automagically place them in East US.
I can use __az config set__ to change this by exiting the __az configure__ command in a key/value pair.
Let's try changing our default location to West Europe:

![changing to westeurope](/azureclitips/images/2.png)

As you can see, my default location changed to West Europe.
We can set other default configuration options such as : Resource Groups, App Service, VM name, VMSS name, Azure Container Registry and more.

__Important Note__ : If you don't like the __az configure__ command, you can write the configuration yourself by editing the Azure CLI config file which exists at : $HOME/.azure/config on Linux and MacOS and %USERPROFILE%/azure if you're using Windows.

__core__ gives you the ability to change Azure CLI's behavior. A good example will be making Azure CLI default to yes on every prompt by adding __disable_confirm_prompt=Yes__ on the Azure CLI configuration file, however, this is not a recommended approach so, __use this for development purposes only__.



## Styling for the fun of it

Azure CLI includes a lot of styling options for having a clean and understandable output.
Back to the __az configure__ command, let's type Y and continue making changes,
Azure CLI will now prompt you for a default output :

![default output](/azureclitips/images/3.png)

As you probably know, by default if not set differently Azure CLI will always return the output as JSON.
Let's look at the following options - __json,jsonc,tsv,yaml,yamlc__ and __table__.

__JSON__ is the default output. Nothing fancy here.

__JSONC__ is an interesting one. It highlights __values__ in __JSON__ format and make them distinct from Dictionary and Array keys :
![JSONC](/azureclitips/images/4.png)

If you like JSON, this will defintely make your work easier.
This one is currently what I use by default.

__YAML__ makes the output return in a yaml format.
__YAMLC__ is the same as JSONC, but for yaml.
Using the same command again :

![YAMLC](/azureclitips/images/5.png)


__TSV__ will make the output return in a tsv format. I don't recommend using this option unless it's mandatory for you.

__table__ is the one to use if you don't need elaborated information. Using the same command again :

![table](/azureclitips/images/6.png)

__Important Note__ : You can always __bypass__ the default configuration for output using __-o__ trigger. 
for example, __az group list -o table__ will always return the output in a table format, regarding of what is set by default.

Choose the one that you like the most, and let's move on.

Next, Azure CLI will ask you if you want to log to file. I recommend __enabling__ this for debugging purposes.
This setting will log  the exit code of your commands to __%HOME%/.azure/commands__ folder on Linux and __%USERPROFILE/.azure/commands__ on Windows :

![log to file](/azureclitips/images/7.png)

__Enabling data collection__ is up to you - nothing to elaborate here.

Do not change the default TTL for __Azure CLI cache__. Here the default approach is great for all scenarios, unless you have a specific requirement.

Great, now Azure CLI is tailored to your needs and you can start enjoying it.


## General Tips


1. Use __--debug__ trigger

If you're running a complex command and you want detailed output, __--debug__ is your friend. 

Use this trigger whenever you want to see how ARM handles your request.
Let's say we're running a complex creation of Azure Red Hat OpenShift.
The basic command is -

` az aro create -n name -g resourcegroup `

This command will not show a lot of information back to the user on a failure.

Add __--debug__ to see everything behind the scenes and then if something fails troubleshooting will be immensly easier :

` az aro create -n name -g resourcegroup --debug`



2. Use __--no-wait__ for long operations

Leverage the __--no-wait__ trigger if your command takes time to complete and you need to run other commands meanwhile.
For example, let's say we're deleting an Azure Kubernetes Service (AKS) cluster :

`az aks delete -n clustername -g resourcegroup`

This command will prompt us to make sure that we wish to accomplish this operation and then will make us wait for it complete.

Add __--no-wait__ and reclaim your terminal while the command continues to run in the background :

`az aks delete -n clustername -g resourcegroup --no-wait`

__Important Note__ : --no-wait trigger will not return any output back, so you need make sure the command did finish in another way.




3. Use __--yes__ for operations that need user prompt

If you're absolutely sure about an operation that requires user prompt, use __--yes__ to bypass Azure CLI's prompt.

Back the __az aks delete__ command, adding __--yes__ will remove the prompt asking us to confirm :

`az aks delete -n clustername -g resourcegroup --no-wait --yes`

Use this __only__ if you're sure of the operation you're confirming.


4. Use __az interactive__ if you're new to Azure CLI

__az interactive__ is a great way to learn Azure CLI. This will install another extension on your workstation,
and will help you writing commands in a nice and clean way :


![interactive](/azureclitips/images/8.png)
