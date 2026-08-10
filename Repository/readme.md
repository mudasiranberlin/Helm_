# 🚀 Helm Repository: Payments & Shipping

This project shows how to create a **Helm Repository** containing two Helm charts:

* 💳 **Payments Service**
* 🚚 **Shipping Service**

We will use the **BusyBox** Docker image as a dummy application for both services.

The Helm charts can then be hosted on **GitHub Pages** and installed using Helm.

---

## 📚 What We Will Learn

In this project, we will learn how to:

1. Create Helm charts
2. Customize Helm charts
3. Deploy applications using Helm
4. Package Helm charts
5. Create a Helm repository
6. Host the repository on GitHub Pages
7. Install charts from our Helm repository

---

# 🏗️ Project Structure

After completing the project, our directory will look similar to this:

```text
helm-repo/
│
├── payments/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       └── deployment.yaml
│
├── shipping/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       └── deployment.yaml
│
├── payments-0.1.0.tgz
├── shipping-0.1.0.tgz
└── index.yaml
```

---

# ✅ Prerequisites

Before starting, make sure you have:

* Helm installed
* kubectl installed
* A running Kubernetes cluster
* A GitHub account
* Git installed

Check Helm:

```bash
helm version
```

Check Kubernetes:

```bash
kubectl version --client
```

Check your cluster:

```bash
kubectl get nodes
```

---

# 1️⃣ Create the Helm Charts

Create a directory for our Helm repository:

```bash
mkdir helm-repo
cd helm-repo
```

Create the Payments chart:

```bash
helm create payments
```

Create the Shipping chart:

```bash
helm create shipping
```

Now we have two Helm charts:

```text
helm-repo/
├── payments/
└── shipping/
```

---

# 2️⃣ Configure the Payments Chart

Go into the Payments chart:

```bash
cd payments
```

Open:

```text
values.yaml
```

Replace the values with:

```yaml
image:
  repository: busybox
  tag: latest
  pullPolicy: IfNotPresent

appMessage: "Payments Service"
```

---

## Payments Deployment

Open:

```text
payments/templates/deployment.yaml
```

You can replace the deployment template with:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: {{ .Release.Name }}-{{ .Chart.Name }}

spec:
  replicas: 1

  selector:
    matchLabels:
      app: {{ .Chart.Name }}

  template:
    metadata:
      labels:
        app: {{ .Chart.Name }}

    spec:
      containers:
        - name: payments

          image: {{ .Values.image.repository }}:{{ .Values.image.tag }}

          command:
            - sh
            - -c
            - "echo {{ .Values.appMessage }}; sleep 3600"

          imagePullPolicy: {{ .Values.image.pullPolicy }}
```

### What does this do?

The container starts BusyBox and runs:

```bash
echo "Payments Service"
```

Then it stays alive for:

```bash
sleep 3600
```

So we can see the container running inside Kubernetes.

---

# 3️⃣ Configure the Shipping Chart

Go back to the main directory:

```bash
cd ..
```

Now enter the Shipping chart:

```bash
cd shipping
```

Open:

```text
values.yaml
```

Use:

```yaml
image:
  repository: busybox
  tag: latest
  pullPolicy: IfNotPresent

appMessage: "Shipping Service"
```

---

## Shipping Deployment

Open:

```text
shipping/templates/deployment.yaml
```

Use:

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: {{ .Release.Name }}-{{ .Chart.Name }}

spec:
  replicas: 1

  selector:
    matchLabels:
      app: {{ .Chart.Name }}

  template:
    metadata:
      labels:
        app: {{ .Chart.Name }}

    spec:
      containers:
        - name: shipping

          image: {{ .Values.image.repository }}:{{ .Values.image.tag }}

          command:
            - sh
            - -c
            - "echo {{ .Values.appMessage }}; sleep 3600"

          imagePullPolicy: {{ .Values.image.pullPolicy }}
```

---

# 4️⃣ Test the Helm Charts

Before packaging the charts, check that they don't contain errors.

Go back to the repository directory:

```bash
cd ..
```

Test Payments:

```bash
helm lint payments
```

Test Shipping:

```bash
helm lint shipping
```

You should see:

```text
1 chart(s) linted, 0 chart(s) failed
```

---

# 5️⃣ See the Kubernetes YAML

Helm can generate the Kubernetes YAML without installing anything.

For Payments:

```bash
helm template payments-service payments
```

For Shipping:

```bash
helm template shipping-service shipping
```

This is very useful for checking what Helm will create.

---

# 6️⃣ Install the Charts

## Install Payments

```bash
helm install payments-service ./payments
```

Check the Helm releases:

```bash
helm list
```

Check the Pods:

```bash
kubectl get pods
```

You should see something similar to:

```text
payments-service-payments-xxxxx   1/1   Running
```

Check the Deployment:

```bash
kubectl get deployments
```

---

## Install Shipping

```bash
helm install shipping-service ./shipping
```

Check:

```bash
helm list
```

Check Pods:

```bash
kubectl get pods
```

You should now have both services running.

---

# 7️⃣ Check the Application Messages

Find the Payments Pod:

```bash
kubectl get pods
```

Then check its logs:

```bash
kubectl logs <payments-pod-name>
```

You should see:

```text
Payments Service
```

For Shipping:

```bash
kubectl logs <shipping-pod-name>
```

You should see:

```text
Shipping Service
```

---

# 8️⃣ Package the Helm Charts

Now we are ready to create Helm packages.

From the `helm-repo` directory:

```bash
helm package payments
```

Output:

```text
Successfully packaged chart and saved it to:
./payments-0.1.0.tgz
```

Package Shipping:

```bash
helm package shipping
```

Output:

```text
Successfully packaged chart and saved it to:
./shipping-0.1.0.tgz
```

Now we have:

```text
helm-repo/
├── payments/
├── shipping/
├── payments-0.1.0.tgz
└── shipping-0.1.0.tgz
```

---

# 9️⃣ Create the Helm Repository Index

Run:

```bash
helm repo index .
```

This creates:

```text
index.yaml
```

Our directory now looks like:

```text
helm-repo/
│
├── payments/
├── shipping/
│
├── payments-0.1.0.tgz
├── shipping-0.1.0.tgz
└── index.yaml
```

### What is `index.yaml`?

`index.yaml` is the **catalog of our Helm repository**.

It tells Helm:

* What charts are available
* Chart versions
* Chart names
* Where the packaged charts are located

Think of it like a **menu for your Helm repository**.

---

# 🔟 Create a GitHub Repository

Create a new GitHub repository called:

```text
helm-repo
```

For example:

```text
https://github.com/YOUR-USERNAME/helm-repo
```

Replace `YOUR-USERNAME` with your GitHub username.

---

# 1️⃣1️⃣ Push the Repository to GitHub

From the `helm-repo` directory:

```bash
git init
```

Add your GitHub repository:

```bash
git remote add origin https://github.com/YOUR-USERNAME/helm-repo.git
```

Add the files:

```bash
git add .
```

Commit:

```bash
git commit -m "Add payments and shipping Helm charts"
```

Rename the branch:

```bash
git branch -M main
```

Push:

```bash
git push -u origin main
```

---

# 1️⃣2️⃣ Enable GitHub Pages

Go to your GitHub repository.

Open:

```text
Settings
   ↓
Pages
```

Under **Build and deployment**:

Select:

```text
Source: Deploy from a branch
```

Select:

```text
Branch: main
Folder: / (root)
```

Click:

```text
Save
```

GitHub will provide a Pages URL similar to:

```text
https://YOUR-USERNAME.github.io/helm-repo/
```

---

# 1️⃣3️⃣ Add the Helm Repository

Now anyone with access to the GitHub Pages repository can add it to Helm.

Run:

```bash
helm repo add myrepo https://YOUR-USERNAME.github.io/helm-repo/
```

Update the repository:

```bash
helm repo update
```

---

# 1️⃣4️⃣ Search the Helm Repository

Run:

```bash
helm search repo myrepo
```

You should see:

```text
NAME              CHART VERSION
myrepo/payments   0.1.0
myrepo/shipping   0.1.0
```

🎉 Our Helm repository is working!

---

# 1️⃣5️⃣ Install Payments from the Repository

Now we don't need to use the local chart.

Install Payments:

```bash
helm install payments-service myrepo/payments
```

Check:

```bash
helm list
```

Check Pods:

```bash
kubectl get pods
```

---

# 1️⃣6️⃣ Install Shipping from the Repository

Run:

```bash
helm install shipping-service myrepo/shipping
```

Check:

```bash
helm list
```

Check Pods:

```bash
kubectl get pods
```

---

# 🔄 Useful Helm Commands

### List Helm releases

```bash
helm list
```

### List all Pods

```bash
kubectl get pods
```

### Check Helm release

```bash
helm status payments-service
```

### Upgrade a release

```bash
helm upgrade payments-service myrepo/payments
```

### Uninstall Payments

```bash
helm uninstall payments-service
```

### Uninstall Shipping

```bash
helm uninstall shipping-service
```

### Update Helm repository

```bash
helm repo update
```

### List Helm repositories

```bash
helm repo list
```

### Remove a Helm repository

```bash
helm repo remove myrepo
```

---

# 🧠 How Everything Works

The complete flow is:

```text
        Helm Chart
            │
            ▼
     payments/
     shipping/
            │
            ▼
      helm package
            │
            ▼
       .tgz files
            │
            ▼
       helm repo index
            │
            ▼
        index.yaml
            │
            ▼
       GitHub Pages
            │
            ▼
      Helm Repository
            │
            ▼
       helm repo add
            │
            ▼
      helm install
            │
            ▼
       Kubernetes
            │
       ┌────┴────┐
       ▼         ▼
   Payments   Shipping
```

---

# 🎯 Important Concepts

| Concept          | Simple Meaning                                          |
| ---------------- | ------------------------------------------------------- |
| Helm             | Package manager for Kubernetes                          |
| Helm Chart       | Package containing Kubernetes application configuration |
| `values.yaml`    | Stores configurable values                              |
| `templates/`     | Contains Kubernetes templates                           |
| `helm package`   | Creates a `.tgz` Helm package                           |
| `index.yaml`     | Catalog of Helm charts                                  |
| Helm Repository  | Place where Helm charts are stored                      |
| GitHub Pages     | Hosts our Helm repository                               |
| `helm repo add`  | Adds a Helm repository                                  |
| `helm install`   | Installs a Helm chart                                   |
| `helm upgrade`   | Updates an installed application                        |
| `helm uninstall` | Removes an application                                  |

---

# 🧹 Cleanup

Remove the applications from Kubernetes:

```bash
helm uninstall payments-service
```

```bash
helm uninstall shipping-service
```

Check:

```bash
kubectl get pods
```

---

# 🚀 Final Result

We created a Helm repository containing:

```text
📦 Helm Repository
│
├── 💳 Payments Chart
│
└── 🚚 Shipping Chart
```

Both charts use:

```text
BusyBox
```

We packaged the charts, generated `index.yaml`, uploaded everything to GitHub, enabled GitHub Pages, and installed the charts from our remote Helm repository.

This gives us a simple foundation for creating and managing **real application Helm repositories** in a DevOps/GitOps environment.
