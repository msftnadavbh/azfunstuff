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

