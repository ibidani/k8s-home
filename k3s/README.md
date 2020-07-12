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
