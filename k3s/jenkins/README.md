## installing Jenkins helm chart
```shell
helm repo add jenkins https://charts.jenkins.io
kubectl create namespace jenkins
helm upgrade --install jenkins jenkins/jenkins -f values.yaml --namespace=jenkins
```