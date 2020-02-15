## Remote Kind k8s cluster

On Kind server:
```
kind create cluster --config=remote-kind-cluster.yaml
```

On kubectl client host:
```
scp <kind_user>@<kind_host>:~/.kube/config ~/.kube/config
