# Helm Installation

## 📌 What is Helm?

**Helm** is a package manager for Kubernetes. It helps you install, upgrade, and manage Kubernetes applications easily.

---

# 🍎 Install Helm on macOS

### Option 1: Homebrew — Recommended

If you have Homebrew installed:

```bash
brew install helm
```

Check the installation:

```bash
helm version
```

### If Homebrew is not installed

Install Homebrew first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then:

```bash
brew install helm
```

---

# 🪟 Install Helm on Windows

## Option 1: Winget — Recommended

Open **PowerShell** or **Command Prompt** and run:

```powershell
winget install Helm.Helm
```

Check the installation:

```powershell
helm version
```

---

## Option 2: Chocolatey

If you have Chocolatey installed:

```powershell
choco install kubernetes-helm
```

Then check:

```powershell
helm version
```

---

# 🐧 Install Helm on Linux

### 1. Download the installation script

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```

### 2. Give permission

```bash
chmod 700 get_helm.sh
```

### 3. Run the script

```bash
./get_helm.sh
```

### 4. Check Helm

```bash
helm version
```

---

# 🧠 Quick Summary

| Operating System | Recommended Command        |
| ---------------- | -------------------------- |
| 🍎 macOS         | `brew install helm`        |
| 🪟 Windows       | `winget install Helm.Helm` |
| 🐧 Linux         | `curl` installation script |

After installation, verify:

```bash
helm version
```

If you see the Helm version, the installation was successful. ✅
