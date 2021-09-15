# Azure CLI Tips & Tricks

## Intro

Overall, most people are aware of the basics of Azure CLI.

e.g listing VMs, getting the running state of a particular resource, etc.

In this article, I'll give you some great tips on enhancing your work with Azure CLI,

Leveraging it's power over basically any other way of interacting with Azure.

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

![az configure](/images/1.png)

Let's run through the stuff here.

__Cloud Name__ basically means the current Azure Cloud that you're using. This is doesn't need to be changed unless you're using Azure Gov.

__defaults__ needs some more elaboration. As you can see, my default location is set to East US. This means if I dont set the -l trigger at resource creation,
Azure CLI will automagically place them in East US.
I can use __az config set__ to change this by exiting the __az configure__ command in a key/value pair.
Let's try changing our default location to West Europe:

![changing to westeurope](/images/2.png)

As you can see, my default location changed to West Europe.
We can set other default configuration options such as : Resource Groups, App Service, VM name, VMSS name, Azure Container Registry and more.

__Important Note__ : If you don't like the __az configure__ command, you can write the configuration yourself by editing the Azure CLI config file which exists at : $HOME/.azure/config on Linux and MacOS and %USERPROFILE%/azure if you're using Windows.

## Styling for the fun of it

Azure CLI includes a lot of styling options for having a clean and understandable output.
Back to the __az configure__ command, let's type Y and continue making changes,
Azure CLI will now prompt you for a default output :

![default output](/images/3.png)

As you probably know, by default if not set differnetly Azure CLI will always return the output as JSON.
Let's look at the following options - __json,jsonc,tsv,yaml,yamlc__ and __table__.

__JSON__ is the default output. Nothing fancy here.

__JSONC__ is an interesting one. It highlights __values__ in __JSON__ format and make them distinct from Dictionary and Array keys :
![JSONC](/images/4.png)

If you like JSON, this will defintely make your work easier.
This one is currently what I use by default.

__YAML__ makes the output return in a yaml format.
__YAMLC__ is the same as JSONC, but for yaml.
Using the same command again :

![YAMLC](/images/5.png)




