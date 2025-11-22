# n8n AWS YAML & Docker Deployment

This repository provides production-ready Kubernetes YAML manifests for deploying **n8n** on AWS-backed Kubernetes clusters.  
It includes both **development** and **production** configurations, making it easy for DevOps teams to bootstrap, customize, and scale a fully operational n8n environment.

---

## Repository Structure

```
.
├── LICENSE
├── README.md
├── dev
│   └── kubeconfig.yaml
└── prod
    └── kubeconfig.yaml
```

- **dev/kubeconfig.yaml**  
  Development environment deployment configuration.

- **prod/kubeconfig.yaml**  
  Production-ready optimized configuration.

---

## What This Deployment Includes

### 1. Kubernetes Service
Exposes n8n internally within the cluster on port **80**, mapping to the container’s port **5678**.

### 2. Ingress (HAProxy)
Configures HTTPS access for n8n using your cluster’s ingress controller.

- Enforces SSL redirect  
- Uses the specified domain  
- Supports TLS via your wildcard certificate

### 3. n8n Deployment
The deployment includes:

- `n8nio/n8n:latest` container  
- Secure config for:
  - Internal/external URLs  
  - SMTP email  
  - Proxy settings (disabled by default in this template)  
  - Trusted proxies  
- Kubernetes health probes  
- Persistent storage using a **PVC**  
- Runners enabled

---

## Important Notes

### Update Required Before Use
Replace all placeholders:

- `PLACEHOLDER_NAMESPACE`
- `PLACEHOLDER_SERVICE_NAME`
- Ingress domains (`n8n.batman.dev.com`)
- SMTP credentials
- Proxy configuration (if needed)

---

## Why This Repository Exists

This template gives DevOps teams a clean, consistent baseline to deploy n8n with Kubernetes.  
It is reusable across environments, supports GitOps workflows, and keeps configuration clean and modular.

---

## Included Kubernetes Objects

- `Service`  
- `Ingress`  
- `Deployment`  
- `PersistentVolumeClaim`

Everything required to run a complete n8n instance inside an AWS EKS or similar cluster.

---

## How to Deploy

### Step 1 — Modify placeholders
Edit the YAML for your cluster naming, domain, namespace, and certificate.

### Step 2 — Apply to your cluster
```
kubectl apply -f dev/kubeconfig.yaml
```

or

```
kubectl apply -f prod/kubeconfig.yaml
```

### Step 3 — Verify deployment
```
kubectl rollout status deployment/<your-n8n-name> -n <namespace>
```

---

## License

This project is licensed under the **MIT License** — free for personal and commercial use.

---

## Author
**Jawwad Ahmed Abbasi**  
Senior Software Developer  
[GitHub](https://github.com/jawwadabbasi) | [YouTube](https://www.youtube.com/@jawwad_abbasi)