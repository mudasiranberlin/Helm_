# Helm Installation on Linux

## 📌 What is Helm?

**Helm** is a package manager for Kubernetes.

It helps you easily install, upgrade, and manage Kubernetes applications.

---

## 🚀 Install Helm

### 1. Download the Helm installation script

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```

### 2. Give permission to the script

```bash
chmod 700 get_helm.sh
```

### 3. Run the installation script

```bash
./get_helm.sh
```

### 4. Check Helm version

```bash
helm version
```

If Helm is installed correctly, you will see the Helm version.

---

## 🧠 Quick Summary

```text
Download
   ↓
Give Permission
   ↓
Run Script
   ↓
Check Version
```

Commands:

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

chmod 700 get_helm.sh

./get_helm.sh

helm version
```
