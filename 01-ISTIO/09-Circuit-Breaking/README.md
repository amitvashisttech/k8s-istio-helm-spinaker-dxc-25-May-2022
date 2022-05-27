# Circuit Breaking

## Deploy httpapp respectivly 

```
kubectl apply -f <(istioctl kube-inject -f http.yaml)
```

# Configuring the circuit breaker

## Create a destination rule to apply circuit breaking settings when calling the httpbin service:
```
kubectl apply -f cb-destination-rule.yaml
```

## Verify the destination rule was created correctly:
```
kubectl get destinationrule httpbin -o yaml
```

## Add a simple load-testing client called fortio. 
```
kubectl apply  -f fortio-deploy.yaml

```

## Now, Log in to the client pod and use the fortio tool to call httpbin. Pass in curl to indicate that you just want to make one call:
```
export FORTIO_POD=$(kubectl get pods -l app=fortio -o 'jsonpath={.items[0].metadata.name}')
kubectl exec "$FORTIO_POD" -c fortio -- /usr/bin/fortio curl -quiet http://httpbin:8000/get
```

## Tripping the circuit breaker

### Call the service with two concurrent connections (-c 2) and send 20 requests (-n 20):
```
kubectl exec "$FORTIO_POD" -c fortio -- /usr/bin/fortio load -c 2 -qps 0 -n 20 -loglevel Warning http://httpbin:8000/get
```

### Now, Bring the number of concurrent connections up to 3: 
```
kubectl exec "$FORTIO_POD" -c fortio -- /usr/bin/fortio load -c 3 -qps 0 -n 30 -loglevel Warning http://httpbin:8000/get

```

### Query the istio-proxy stats to see more:

```
kubectl exec "$FORTIO_POD" -c istio-proxy -- pilot-agent request GET stats | grep httpbin | grep pending
```



## Clean up
```
kubectl delete destinationrule httpbin

```

## Remove the deployment
```
kubectl delete deploy httpbin fortio-deploy
kubectl delete svc httpbin fortio
```
