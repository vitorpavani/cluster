# cluster

## 1. Create a cluster

### 1.1 Create a cluster with kind

First we need to install the cluster. We will use [kind](https://kind.sigs.k8s.io/) to create a local cluster.

```
kind create cluster --config kind/cluster.yaml
```

## 2. Install ArgoCD

### 2.1 Install ArgoCD with manifests

First apply namespace.

```
kubectl apply -f argocd/argocd-ns.yaml
```

Then install ArgoCD.

```
kubectl apply -n argocd -f argocd/install.yaml
```

Add the ArgoCD repo and Cluster Application.

```
kubectl apply -n argocd -f argocd/configs/
```

### 2.2 Access ArgoCD

First we need to get the password.

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Then we can access ArgoCD with the password.

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
