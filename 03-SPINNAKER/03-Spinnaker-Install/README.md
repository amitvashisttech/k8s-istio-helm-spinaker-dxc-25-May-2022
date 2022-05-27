# Deploying Spinnaker in a Kubernetes cluster

### Pre-requisites
Kubernetes cluster with atleast **6 cores** and **20GB memory**


#### Start Halyard Container

```
mkdir ~/.hal
docker run --name halyard -v ~/.hal:/home/spinnaker/.hal -v ~/.kube/config:/home/spinnaker/.kube/config -d gcr.io/spinnaker-marketplace/halyard:stable
```

Get a shell into Halyard container
```
docker exec -it halyard bash
```

### Below commands are to be run inside the halyard container

Check if you can run kubectl commands
```
kubectl cluster-info
```

#### Set Kubernetes as the cloud provider
```
hal config provider kubernetes enable
```

#### Add a kubernetes account
```
hal config provider kubernetes account add my-k8s --provider-version v2 --context $(kubectl config current-context)
```

#### Enable artifacts
```
hal config features edit --artifacts true
```

#### Choose where to install Spinnaker
```
hal config deploy edit --type distributed --account-name my-k8s
```

### Below command needs to be run on your local machine where you have helm binary
#### Install acs in kubernetes cluster
```
```

#### Choose spinnaker version to install
```
hal version list
hal config version edit --version <desired-version>
```

#### All Done! Deploy Spinnaker in Kubernetes Cluster
```
hal deploy apply
```

#### Change the service type to either Load Balancer or NodePort
```
kubectl -n spinnaker edit svc spin-deck
kubectl -n spinnaker edit svc spin-gate
```

#### Update config and redeploy
```
hal config security ui edit --override-base-url "http://<LoadBalancerIP>:9000"
hal config security api edit --override-base-url "http://<LoadBalancerIP>:8084"
hal deploy apply
```
*If you used NodePort*
```

hal config security ui edit --override-base-url "http://<worker-node-ip>:<nodePort>"
hal config security api edit --override-base-url "http://worker-node-ip>:<nodePort>"
hal deploy apply
```
