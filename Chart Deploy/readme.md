# Managing NGINX with Helm

Helm makes it easy to **install, upgrade, and remove NGINX** on Kubernetes.

## Prerequisites

* Kubernetes cluster running
* `kubectl` installed
* Helm installed

## 1. Install NGINX

Add the Bitnami repository:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

Install NGINX:

```bash
helm install my-nginx bitnami/nginx
```

Check:

```bash
helm list
kubectl get pods
```

## 2. Customize NGINX

See available settings:

```bash
helm show values bitnami/nginx
```

Preview the Kubernetes YAML:

```bash
helm template my-nginx bitnami/nginx
```

## 3. Upgrade NGINX

Change the service to NodePort:

```bash
helm upgrade my-nginx bitnami/nginx --set service.type=NodePort
```

Check the status:

```bash
helm status my-nginx
```

## 4. Uninstall NGINX

Remove NGINX:

```bash
helm uninstall my-nginx
```

Check:

```bash
helm list
kubectl get pods
```

### Simple Helm Flow

```text
helm install   → Install NGINX
helm upgrade   → Change NGINX
helm status    → Check NGINX
helm uninstall → Remove NGINX
```
