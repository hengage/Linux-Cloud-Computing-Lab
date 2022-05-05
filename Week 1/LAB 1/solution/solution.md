# Solution To Lab Task

I used the azure CLi loccally because the azure cloud CLi required a subscription.

## Steps

1. I logged into the azure cLI using: `az login`

2. Then i created a resource group with the appropriate command: `az group create --name schulltech --location australiaeast`

3. Next I created a virtual machine: `az vm create -name schulltech -resource-group schulltech --admin-username hengage --image Ubuntu LTS --generate-ssh-keys`

4. After that I opened a port 80: `az vm open=port --port 80 -g schulltech -n schulltech`

5. i connected to the port 80 to my vm using ssh and my vm's public address: `ssh hengage@52.187.201.165`

6. lastly, i updated packages and installed the web server: `sudo apt-get -y update` and
   `sudo apt-get -y install nginx`

Look in the 'solution_screenshots' folder for photos of some of the steps i took and the final web server.
