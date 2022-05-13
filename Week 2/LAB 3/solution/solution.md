# Solution To Week Lab 3 Task

I used the azure CLi loccally because the azure cloud CLi required a subscription.

## Steps

1. I logged into the azure cLI using: `az login`

2. I created a resource group: `az group create --name schulltech --location australiaeast`

3. I created a virtual machine using the resource group: `az vm create -name schulltech -resource-group schulltech --admin-username hengage --image Ubuntu LTS --generate-ssh-keys`
