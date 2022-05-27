1800  cd istio-1.13.4/
 1801  ls
 1802  kubectl apply -f samples/addons 
 1803  kubectl get status 
 1804  kubectl get pods 
 1805  kubectl get ns 
 1806  kubectl get pods -n istio-system
 1807  kubectl get svc  -n istio-system
 1808  kubectl edit svc kiali -n istio-system
 1809  kubectl get svc  -n istio-system
 1810  curl -vv http://20.241.130.182/productpage
 1811  for i in $(seq 1 200); do curl -s -o /dev/null "http://20.241.130.182/productpage"; done 
 1812  for i in $(seq 1 200); do curl -s -o /dev/null "http://20.241.130.182/hello"; done 
 1813  ls
 1814  cd ../
 1815  ls
 1816  cd k8s-istio-helm-spinaker-dxc-25-May-2022/
 1817  ls
 1818  cd 02-HelloWorld/
 1819  ls
 1820  cat 04-hello-v2.yaml 
 1821  kubectl  apply -f 04-hello-v2.yaml 
 1822  kubectl  get pods 
 1823  curl http://20.241.130.182/hello
 1824  for i in $(seq 1 200); do curl -s -o /dev/null "http://20.241.130.182/hello"; done 
