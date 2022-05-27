# Install AKS Cluster 

```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az provider show -n Microsoft.OperationsManagement -o table
Namespace                       RegistrationPolicy    RegistrationState
------------------------------  --------------------  -------------------
Microsoft.OperationsManagement  RegistrationRequired  Registered
```

## Creating a dedicated Resource Group
```
$ az group create --name myaksrg --location eastus
{
  "id": "/subscriptions/8d1383e9-dfb2-4723-97ed-6ca7a041b758/resourceGroups/myaksrg",
  "location": "eastus",
  "managedBy": null,
  "name": "myaksrg",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```

## Setup 1 Node AKS Cluster with Standard_D4_v2
```
az aks create --resource-group myaksrg --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys --node-vm-size Standard_D4_v2
 
 ```

## Configure Kubeconfig to intract with AKS 
```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az account set --subscription 8d1383e9-dfb2-4723-97ed-6ca7a041b758
```
 
```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az aks get-credentials --resource-group myaksrg --name myAKSCluster
```

## Let's check the K8s Cluster Status
```
kubectl get ns 
```
 
