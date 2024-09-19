## ArgoCD GitOps Example Project

## Project Description

This project demonstrates the implementation of GitOps principles using ArgoCD in a Kubernetes environment. GitOps is an operational framework that takes DevOps best practices used for application development such as version control, collaboration, compliance, and CI/CD, and applies them to infrastructure.

This project serves as a practical example of how to set up and use ArgoCD to implement these GitOps principles in a Kubernetes environment. By following this README, you'll be able to set up a local Minikube cluster, install ArgoCD, and deploy an application using GitOps practices.

## Prerequisites

- macOS with ARM64 architecture
- `kubectl` command-line tool
- Internet connection

## Steps

### 1. Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-arm64
sudo install minikube-darwin-arm64 /usr/local/bin/minikube
```

### 2. Start Minikube

```bash
minikube start
```

### 3. Verify Minikube Installation

```bash
kubectl get pods -A
```

### 4. Install ArgoCD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 5. Monitor ArgoCD Pod Status

```bash
kubectl get pods -n argocd -w
```

### 6. Check ArgoCD Services

```bash
kubectl get svc -n argocd
```

### 7. Edit ArgoCD Server Service (Optional)

If you need to modify the ArgoCD server service:

```bash
kubectl edit svc argocd-server -n argocd
```

### 8. List Minikube Services

```bash
minikube service list -n argocd
```

### 9. Access ArgoCD UI

```bash
minikube service argocd-server -n argocd
```

This command will open the ArgoCD UI in your default web browser.

### 10. Create an Application in ArgoCD

1. Access the ArgoCD UI using the URL provided by the previous command.
2. Log in using the default admin account. To get the password:
   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
   ```
3. Click on "New App" in the UI.
4. Fill in the application details:
   - Application Name: Choose a name for your application
   - Project: default
   - Sync Policy: Choose as needed
   - Repository URL: Your GitHub repository URL
   - Path: Path to your Kubernetes manifests in the repo
   - Cluster: https://kubernetes.default.svc
   - Namespace: Choose as needed
5. Click "Create" to create the application.

### 11. Deploy the Application

In the ArgoCD UI, find your newly created application and click "Sync" to deploy it.

## Conclusion

You have now successfully set up ArgoCD on Minikube and deployed an application using manifest files from a GitHub repository. Monitor the application status in the ArgoCD UI to ensure successful deployment.