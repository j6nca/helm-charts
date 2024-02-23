# argo-cd

## Setup

```
helm repo add argo-cd https://argoproj.github.io/argo-helm
helm dep update helm/argo-cd/
helm install argo-cd helm/argo-cd/ --create-namespace -n argocd 
```

## Load UI

```
kubectl port-forward svc/argo-cd-argocd-server 8080:443
```

## Cleanup

On deletion, remove CRDs and secrets
```
kubectl delete crd applications.argoproj.io
kubectl delete crd applicationsets.argoproj.io
kubectl delete crd appprojects.argoproj.io
kubectl delete secret argocd-initial-admin-secret
```