# Lab 3: GCP

## Compute Engine

### Tutorials
[ Quickstart using a Linux VM](https://cloud.google.com/compute/docs/create-linux-vm-instance)

[Connect to Linux VMs](https://cloud.google.com/compute/docs/instances/connecting-to-instance)

[Connecting to Linux VMs using advanced methods](https://cloud.google.com/compute/docs/instances/connecting-advanced)

[Using startup scripts on Linux VMs](https://cloud.google.com/compute/docs/instances/startup-scripts/linux)

[Querying VM metadata](https://cloud.google.com/compute/docs/metadata/querying-metadata)

## gcloud
===========

 Understanding commands


###The gcloud command format. 
gcloud + release level (optional) + component + entity + operation + positional args + flags

###Example gcloud command for creating a virtual machine instance.
gcloud compute instances create <instance_name> --zone=<zone>

## Running commands
*#Get the gcloud help information.* \\

gcloud help

*#Get the gcloud cheat sheet.*

gcloud cheat-sheet

*#Get projects help information.*

gcloud projects --help

*#Get projects create help information.*

gcloud projects create --help

*#Create a new project and set as default.* 

gcloud projects create <project_id> --name=<project_name> --set-as-default

*#List the available billing accounts.*
gcloud beta billing accounts list

###Link a billing account with the project. 
gcloud beta billing projects link <project_id> --billing-account=<account_id>

###List the available services, filter on the name 'compute', and echo the result.    
SERVICE=$(gcloud services list --available --filter="NAME ~ ^compute" --format="value(NAME)")
echo $SERVICE

###Enable the Compute Engine API. 
gcloud services enable $SERVICE

###Set the preferred Compute Engine region. 
gcloud config set compute/region <region>

###Set the preferred Compute Engine zone. 
gcloud config set compute/zone <zone>

###List the current configuration. 
gcloud config list

###List the current networks.
gcloud compute networks list

###List the current firewall rules.
gcloud compute firewall-rules list

###Delete the firewall rules.  
gcloud compute firewall-rules delete default-allow-icmp default-allow-internal default-allow-rdp default-allow-ssh

###Delete the default network.
gcloud compute networks delete default

###Create a custom mode network. 
gcloud compute networks create vpc-network --subnet-mode=custom

<!-- # Create a default subnet.  --> 
gcloud compute networks subnets create default --network=vpc-network --range=10.0.1.0/24
<!-- # Add the external IP from the Cloud Shell session to a variable, add the CIDR notation, and echo the result. --> 
SHELL_EXTERNAL_IP=$(curl ifconfig.co)
SHELL_EXTERNAL_IP="$SHELL_EXTERNAL_IP""/32"
echo $SHELL_EXTERNAL_IP


###Create a firewall rule for SSH traffic.
gcloud compute firewall-rules create allow-ssh-ingress \
  --network=vpc-network \
  --priority=1000 \
  --direction=INGRESS \
  --action=ALLOW \
  --target-tags=ssh \
  --source-ranges=$SHELL_EXTERNAL_IP \
  --rules=tcp:22

###Create a firewall rule for web traffic. 
gcloud compute firewall-rules create allow-web-ingress \
  --network=vpc-network\
  --priority=1000 \
  --direction=INGRESS \
  --action=ALLOW \
  --target-tags=web \
  --source-ranges=0.0.0.0/0 \
  --rules=tcp:80,tcp:443 

###Create a service account. 
gcloud iam service-accounts create web-instance-01 --display-name=web-instance-01 

###Add the email address of the service account to a variable and echo the result. 
SERVICE_ACCOUNT=$(gcloud iam service-accounts list --filter="email ~ ^web-instance-01" --format="value(email)")
echo $SERVICE_ACCOUNT

###Create the instance, including a startup script.
gcloud compute instances create web-instance-01 \
  --machine-type=e2-micro \
  --description="Web server" \
  --image-project=ubuntu-os-cloud \
  --image-family=ubuntu-2004-lts \
  --network=vpc-network \
  --subnet=default \
  --service-account=$SERVICE_ACCOUNT \
  --tags=ssh,web \
 

###Connect to the instance over SSH. 
gcloud beta compute ssh web-instance-01
###Verify that the Apache HTTP Server service is active (running). 
systemctl status apache2.service

*#Verify the custom index.html file.*
cat /var/www/html/index.html

###Close the SSH connection.

exit

###Add the external IP from the instance to a variable, add the HTTP protocol, and echo the result.

HTTP_ADDRESS=$(gcloud compute instances describe web-instance-01 --format="value(networkInterfaces[0].accessConfigs[0].natIP)")
HTTP_ADDRESS="http://""$HTTP_ADDRESS"
echo $HTTP_ADDRESS

###Verify if the instance is reachable
curl $HTTP_ADDRESS

###Stop the instance.
gcloud compute instances stop web-instance-01

### More information
[Free Trial and Free Tier](https://cloud.google.com/free)

[Compute Engine documentation](https://cloud.google.com/compute/docs)

[Cloud Shell documentation](https://cloud.google.com/shell/docs)

[Cloud SDK documentation](https://cloud.google.com/sdk/docs)

[The gcloud tool overview](https://cloud.google.com/sdk/gcloud)

[The gcloud cheat sheet](https://cloud.google.com/sdk/docs/cheatsheet)

[The gcloud cheat sheet: Understanding commands](https://cloud.google.com/sdk/docs/cheatsheet#understanding_commands)