# Steps to get argocd running

## Create namespace and install argocd
* kubectl create namespace argocd
*kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## Login to the UI after portforwarding
kubectl port-forward svc/