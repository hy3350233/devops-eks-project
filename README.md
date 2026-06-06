# DevOps EKS GitOps Project

## Technologies
- AWS EKS
- Terraform
- Kubernetes
- Argo CD
- NGINX
- Prometheus
- Grafana
- GitHub

## Architecture

Terraform → AWS EKS
GitHub → ArgoCD → Kubernetes
Prometheus → Grafana Monitoring

## Deployment

terraform init
terraform apply

kubectl apply -f kubernetes/nginx/

kubectl apply -f argocd/application.yaml


## Install NGINX Ingress Controller

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
--namespace ingress-nginx \
--create-namespace

kubectl get pods -n ingress-nginx

## Install Argo CD
kubectl apply -n argocd \
-f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl get pods -n argocd

## Get ArgoCD Password
kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 -d

kubectl port-forward svc/argocd-server \
-n argocd 8080:443
#https://localhost:8080

## Connect ArgoCD to GitHub 
kubectl apply -f argocd/application.yaml
kubectl get applications -n argocd

## Monitoring Stack
# Install Prometheus + Grafana:
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack \
--namespace monitoring \
--create-namespace

kubectl get pods -n monitoring
kubectl get svc -n ingress-nginx

## Access Grafana
kubectl port-forward svc/monitoring-grafana -n monitoring 3000:80

open## http://localhost:3000

## Author

Himanshu Yadav
