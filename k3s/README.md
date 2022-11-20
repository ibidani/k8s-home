## Remote k3s k8s cluster

Quick install:
```shell
curl -sfL https://get.k3s.io | sh -
```
Installation using k3sup
```shell
k3sup install --ip $IP --user idan --k3s-version v1.24.7+k3s1 --k3s-extra-args '--cluster-domain k3s.ibidani.com --disable metrics-server'
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
Before starting we may want to set --node-external-ip <external-ip> in the /etc/systemd/system/k3s.service
```shell
vim /etc/systemd/system/k3s.service
sudo systemctl daemon-reload
```
```shell
sudo systemctl start k3s
```

## To install cert-manager 
```shell
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm upgrade --install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --version v1.10.0 \
  --set installCRDs=true \
  --set 'extraArgs={--dns01-recursive-nameservers-only,--dns01-recursive-nameservers=8.8.8.8:53\,1.1.1.1:53}'
```

## To setup DNS challenge via Cloudflare
```shell
# https://cert-manager.io/docs/configuration/acme/dns01/cloudflare/
```
## enable traefik dashboard on k3s and persistent
# https://forums.rancher.com/t/k3s-traefik-dashboard-activation/17142/9 

## To setup tls cert with letsencrypt and nginx
https://docs.bitnami.com/tutorials/secure-kubernetes-services-with-ingress-tls-letsencrypt

## To setup tls cert with letsencrypt and traefik

These steps working but require CRD changes and to open port on network for the tlschallenge
TODO: it might be worth to try editing the deployment.yaml with dnschallenge instead 
```shell
# k apply the crd deployment and services 
k apply -f crd.yaml -f deployment.yaml -f services.yaml
# on the k3s server run 
kubectl port-forward --address 0.0.0.0 service/traefik 8000:8000 8080:8080 4443:4443 -n default
# on the Router map 4443 to 443 and internal IP of the k3s server
k apply -f ingressroutes-demo.yml
```


```shell
kubectl create secret generic godaddy-key --from-literal=godaddy-key=dKD3BoJRF2Z6_PMuExtL3QhPePNJeyLn17j
kubectl create secret generic godaddy-secret --from-literal=godaddy-secret=Qj17RvybQGj5k3uETsRfRa

```