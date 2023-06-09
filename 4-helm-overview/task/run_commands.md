## Run and deploy guide

## Run cluster
minikube start --driver=docker

minikube tunnel

# Cluster info
kubectl cluster-info

# show the dashboard
minikube dashboard

# cd to ./helm

## Creating a Chart
helm create users-ms
helm create posts-ms

## Helm Lint
helm lint ./users-ms
helm lint ./posts-ms

## Helm Template
helm template ./users-ms
helm template ./posts-ms

## Helm Get
helm ls --all --namespace=k8s-program


## Helm Install
helm install users-ms ./users-ms --namespace=k8s-program
helm install posts-ms ./posts-ms --namespace=k8s-program


## Helm Upgrade
helm upgrade users-ms ./users-ms --namespace=k8s-program
helm upgrade posts-ms ./posts-ms --namespace=k8s-program

## Helm Rollback
helm rollback users-ms 1 --namespace=k8s-program
helm rollback posts-ms 1 --namespace=k8s-program

## Helm Package
helm package ./users-ms
helm package ./posts-ms

## Helm Repo, Link: https://www.opcito.com/blogs/creating-helm-repository-using-github-pages
helm repo index users-ms --url=https://github.com/hakobhn/helm-charts.git
helm repo index posts-ms --url=https://github.com/hakobhn/helm-charts.git
helm repo update
helm repo list
helm repo add users-ms https://hakobhn.github.io/helm-charts/
helm repo add posts-ms https://hakobhn.github.io/helm-charts/

## Helm uninstall
helm uninstall users-ms --namespace=k8s-program
helm uninstall posts-ms --namespace=k8s-program

## For checking # For emptying the cluster
kubectl get deployments --namespace=k8s-program

## Expose services to the outside of cluster
kubectl expose deployment users-ms --namespace=k8s-program --type=NodePort --port=8080
kubectl expose deployment posts-ms --namespace=k8s-program --type=NodePort --port=8081

## All exposed ports
kubectl describe service --namespace=k8s-program

## For emptying the cluster
kubectl delete all --all --namespace=k8s-program


## Delete cluster data
helm uninstall users-ms --namespace=k8s-program
helm uninstall posts-ms --namespace=k8s-program
kubectl delete all --all --namespace=k8s-program
kubectl delete pvc --all --namespace=k8s-program
kubectl delete configmap --all --namespace=k8s-program
kubectl delete secret --all --namespace=k8s-program

## Remove configmaps
kubectl delete configmap --all --namespace=k8s-program

## Remove secrets
kubectl delete secret --all --namespace=k8s-program

## Delete minikube with cached images
minikube delete
