
Note: Istio requires a running kubernetes cluster and helm. If you don't already have a running Kubernetes cluster, check out the minikube install guide.

## Install and setup Helm Package Manager

```
wget https://storage.googleapis.com/kubernetes-helm/helm-v2.12.2-linux-amd64.tar.gz
tar -zxvf helm-v2.12.2-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm
kubectl -n kube-system create sa tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller
```
## Download & Install Istion Latest version

```
curl -L https://git.io/getLatestIstio | sh -

// version can be different as istio gets upgraded
cd istio-*

sudo mv -v bin/istioctl /usr/local/bin/

```
## Install istio CRD

```
helm install install/kubernetes/helm/istio-init --name istio-init --namespace istio-system

```

##  Cd to downloaded istio directory and create install istio

```
cd istio-*

helm install install/kubernetes/helm/istio --name istio --namespace istio-system --set global.configValidation=false --set sidecarInjectorWebhook.enabled=false --set grafana.enabled=true --set servicegraph.enabled=true

```

## Verification
```
kubectl get pods -n istio-system

```
