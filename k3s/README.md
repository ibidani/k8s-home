## Remote k3s k8s cluster

Quick install:
```shell
curl -sfL https://get.k3s.io | sh -
```

On kubectl client host:
```shell
scp <k3s_user>@<k3s_host>:/etc/rancher/k3s/k3s.yaml ~/.kube/config
```
To stop k3s
```shell
k3s-killall.sh
sudo systemctl stop k3s
```
To start k3s
```shell
sudo systemctl start k3s
```


To setup tls cert with letsencrypt
```shell
# k apply the crd deployment and services 
k apply -f crd.yaml deployment.yaml services.yaml
# on the k3s server run 
kubectl port-forward --address 0.0.0.0 service/traefik 8000:8000 8080:8080 4443:4443 -n default
# on the Router map 4443 to 443 and internal IP of the k3s server
k apply -f ingressroutes-demo.yml
```