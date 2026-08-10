# What is Helm?

## 🚀 Helm: The APT for Kubernetes

**Helm is a package manager for Kubernetes.**

Think of Helm like **APT on Linux**:

```text
Linux                  Kubernetes
  ↓                       ↓
 APT                     Helm
  ↓                       ↓
Packages               Helm Charts
  ↓                       ↓
Install software       Install applications
```

For example, on Linux:

```bash
sudo apt install nginx
```

With Helm:

```bash
helm install my-nginx bitnami/nginx
```

Helm takes a **Helm Chart** and uses it to create Kubernetes resources such as:

* Pods
* Deployments
* Services
* ConfigMaps
* Secrets

---

# 📦 What is a Helm Chart?

A **Helm Chart** is a package containing the files needed to deploy an application to Kubernetes.

For example:

```text
my-chart/
├── Chart.yaml
├── values.yaml
└── templates/
    ├── deployment.yaml
    └── service.yaml
```

Instead of manually creating many Kubernetes YAML files, Helm packages them together.

---

# Why Use Helm?

## 1. 📦 Package Management

APT manages Linux packages.

```bash
sudo apt install nginx
```

Helm manages Kubernetes applications using Charts.

```bash
helm install my-nginx bitnami/nginx
```

---

## 2. 🔢 Version Management

Helm allows you to install a specific Chart version:

```bash
helm install my-nginx bitnami/nginx --version 13.0.0
```

You can also upgrade or roll back applications.

```bash
helm upgrade my-nginx bitnami/nginx
```

```bash
helm rollback my-nginx 1
```

---

## 3. ⚙️ Configuration

Helm allows you to customize an application using `values.yaml`.

For example:

```bash
helm install my-nginx bitnami/nginx --values custom-values.yaml
```

You can change things such as:

* Number of replicas
* Container image
* Service type
* CPU and memory
* Application settings

---

## 4. 🔄 Reusable Deployments

Without Helm, you may need to manage many YAML files manually.

With Helm:

```text
Helm Chart
    ↓
values.yaml
    ↓
Kubernetes Resources
    ↓
Application
```

The same Chart can be used for different environments:

```text
Development
     ↓
   Helm
     ↓
Staging
     ↓
   Helm
     ↓
Production
```

Only the configuration values may change.

---

# 🧠 Helm in Simple Words

Think about installing a **restaurant**.

Without Helm:

```text
Order table
Order chairs
Order kitchen
Order lights
Order equipment
Configure everything
```

With Helm:

```text
        Helm Chart
             ↓
      "Install Restaurant"
             ↓
       Everything Setup
```

Helm packages all the Kubernetes resources needed for an application and makes them easier to install, configure, upgrade, and remove.

---

# 🔥 Important Helm Commands

Install an application:

```bash
helm install my-nginx bitnami/nginx
```

List installed applications:

```bash
helm list
```

Upgrade:

```bash
helm upgrade my-nginx bitnami/nginx
```

Rollback:

```bash
helm rollback my-nginx 1
```

Uninstall:

```bash
helm uninstall my-nginx
```

---

# 🎯 Remember

```text
APT
 ↓
Linux Packages
 ↓
Install Software
```

```text
HELM
 ↓
Helm Charts
 ↓
Kubernetes Resources
 ↓
Install Applications
```

### One-line definition:

> **Helm is a package manager for Kubernetes that uses Helm Charts to install, configure, upgrade, and manage applications.**
