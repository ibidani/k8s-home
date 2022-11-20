## installing Depedency-Track helm chart
```shell
helm repo add evryfs-oss https://evryfs.github.io/helm-charts/
helm repo up
kubectl create namespace dependency-tracker
kubectl config set-context --current --namespace=dependency-tracker
helm upgrade --install dep-track evryfs-oss/dependency-track -f values.yaml
echo "Initial password is admin/admin"
```
