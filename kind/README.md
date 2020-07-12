## Remote Kind k8s cluster

On Kind server:
```
kind create cluster --config=remote-kind-cluster.yaml
```

On kubectl client host:
```
scp <kind_user>@<kind_host>:~/.kube/config ~/.kube/config
```
To setup [Project Contour](https://projectcontour.io/) Ingress run the following
```
 kubectl apply -f https://projectcontour.io/quickstart/contour.yaml
 kubectl patch daemonsets -n projectcontour envoy -p '{"spec":{"template":{"spec":{"nodeSelector":{"ingress-ready":"true"},"tolerations":[{"key":"node-role.kubernetes.io/master","operator":"Equal","effect":"NoSchedule"}]}}}}'
```
