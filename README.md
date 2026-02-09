# Hi, I'm Pranaw Raj Kafle 👋
### DevOps Engineer | GitOps Enthusiast | Infrastructure Architect

I build production-grade, self-healing infrastructure. My work focuses on bridging the gap between development and operations through **Declarative GitOps**, **Zero-Trust Security**, and **Secret Orchestration**.

- 📍 Kathmandu, Nepal
- 💼 DevOps Engineer at **Trust Bridge Capital**
- 🎓 Final Year Computer Engineering at **Kathmandu University**
- 🌐 [pranawrajkafle.com.np](https://www.pranawrajkafle.com.np/)

---

## 🏗️ Current Lab Architecture (K3s + GitOps)
I manage a personal high-availability lab on resource-constrained hardware (4GB RAM), utilizing K3s and Containerd for maximum efficiency.



```mermaid
graph TD
    subgraph GitHub_Cloud
        Code[App Code] -->|Push| CI[GitHub Actions/Jenkins]
        CI -->|Build & Push| DH[DockerHub/GHCR]
        Manifest[Manifest Repo] -->|Sync| ArgoCD
    end

    subgraph K3s_Cluster_Home_Lab
        ArgoCD[ArgoCD Controller] -->|Deploy| Pods[Application Pods]
        Vault[HashiCorp Vault] -->|Inject Secrets| ESO[External Secrets Operator]
        ESO -->|Create| K8sSecret[Native K8s Secrets]
        Pods -->|Read| K8sSecret
        Traefik[Traefik Ingress] -->|Route| Pods
    end

    Cloudflare[Cloudflare Tunnel] -->|Secure Tunnel| Traefik
    Internet((Internet)) -->|HTTPS| Cloudflare
