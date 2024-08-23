# VM

### Create an Azure Virtual Machine.
az vm create --name
             --resource-group
             
### Create a default Ubuntu2204 VM with automatic SSH authentication.
az vm create -n MyVm -g MyResourceGroup --image Ubuntu2204

### Create a default Windows Server VM with a private IP address.
az vm create -n MyVm -g MyResourceGroup --public-ip-address "" --image Win2012R2Datacenter

### Create a VM from a custom managed image.
az vm create -g MyResourceGroup -n MyVm --image MyImage

### Delete a VM.
az vm delete [--force-deletion]
             [--ids]
             [--name]
             [--no-wait]
             [--resource-group]
             [--subscription]
             [--yes]
             
### Delete a VM without a prompt for confirmation.
az vm delete -g MyResourceGroup -n MyVm --yes

### Delete all VMs in a resource group.
az vm delete --ids $(az vm list -g MyResourceGroup --query "[].id" -o tsv)

### List all VMs.
az vm list [--resource-group]
           [--show-details]
           [--vmss]

az vm list -g MyResourceGroup -d

### List available sizes for VMs.
az vm list-sizes [--ids]
                 [--location]
                 [--subscription]

### Get details for compute-related resource SKUs.
az vm list-skus -l westus

az vm open-port -g MyResourceGroup -n MyVm --port 555,557-559 --priority 100

### Start a stopped VM.
az vm start [--ids]
            [--name]
            [--no-wait {0, 1, f, false, n, no, t, true, y, yes}]
            [--resource-group]
            [--subscription]
            
az vm start -g MyResourceGroup -n MyVm

### Power off (stop) a running VM.
az vm stop [--ids]
           [--name]
           [--no-wait]
           [--resource-group]
           [--skip-shutdown]
           [--subscription]

az vm stop --resource-group MyResourceGroup --name MyVm

