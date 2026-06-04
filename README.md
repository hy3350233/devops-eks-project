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

## Monitoring

Prometheus + Grafana

## Author

Himanshu Yadav
