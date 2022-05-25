# Install AKS Cluster 

```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az provider show -n Microsoft.OperationsManagement -o table
Namespace                       RegistrationPolicy    RegistrationState
------------------------------  --------------------  -------------------
Microsoft.OperationsManagement  RegistrationRequired  Registered
```

```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az group create --name myaksrg --location eastus
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
```
amit@Azure:~/k8s-istio-helm-spinaker-dxc-25-May-2022$ az aks create --resource-group myaksrg --name myAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
 \ Running ..
 
 ```
 
