# GitOps HTML App with ArgoCD

## Steps:

### 1. Build and Push Docker Image
```bash
cd app
docker build -t sohel7866/gitops-html:v1.0.0 .
docker push sohel7866/gitops-html:v1.0.0
```

### 2. Install ArgoCD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 3. Access ArgoCD
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### 4. Create Namespace and Apply Application
```bash
kubectl create namespace gitops-html
kubectl apply -f argocd/application.yaml -n argocd
```

### 5. Access App
```bash
minikube service gitops-html -n gitops-html
```
