# RogueLearn.Kubernetes
This repository contains all the K8s manifests of RogueLearn

---
# Set up NGINX Ingress
- Prequisites: [kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/), Cluster (up and running), [Helm](https://helm.sh/) (optional)
- Using Kubectl
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.4/deploy/static/provider/cloud/deploy.yaml
```

- Using Helm
```bash
# Add repo
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

# Install
helm install nginx-ingress ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace
```

- Wait for it to be ready (might took some time)
```bash
kubectl wait --namespace ingress-nginx \
  --for=condition=ready pod \
  --selector=app.kubernetes.io/component=controller \
  --timeout=120s
```

- Verify NGINX is running
```bash
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx
```
