# Solution To Lab 2 Task

As in Lab 1, i created a resource group and vm

## Understanding visual machine images

A virtual machine image is a template which contains software configuration and an operating system.

Vm images comes in different formats

## Understanding virtual machine size

A vm size refers to the qmount of computing resources and memeory a vm has. It needs to be adequate for it's workload.

## Virtual machine power states

Virtual machine power states represents the current state of the vm.

The power states of a vm includes, starting, running, stopping, stopped, deallocating, deallocated.

To find the power state of a vm, we can use the following command

`vm get-instance-view -n my-vm-name -g my-resource-group --query instanceView.statuses[1] --output table`

## Management tasks

Management tasks are tasks like starting, stopping, or deleting a vm.

For example, the following command can be used to stop a virtual machine:

`az vm stop --resource-group myResourceGroupVM --name myVM`
