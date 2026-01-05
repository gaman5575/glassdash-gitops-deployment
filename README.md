# GlassDash GitOps Deployment

Multi-page glassmorphism admin dashboard deployed declaratively using ArgoCD on Minikube.

## Features
- 6+ interconnected HTML pages (Dashboard, Analytics, Users, Settings, Login, Register)
- Shared CSS/JS for consistent styling and interactivity
- Pure GitOps: entire site stored in immutable ConfigMap
- Automatic sync + pod recreation on Git changes

## Architecture

```mermaid
graph TD
    A[GitHub Repo<br>(public/ + manifests/)] -->|ArgoCD Watches| B(ArgoCD Controller)
    B -->|Auto Sync| C[Kubernetes Cluster<br>(Minikube)]
    C --> D[Namespace: glassdash]
    D --> E[Immutable ConfigMap<br>(All static files)]
    D --> F[Deployment<br>(Nginx Pod)]
    F -->|Mounts Volume| E
    F --> G[Service<br>(NodePort)]
    H[Browser] -->|Port-Forward| G
