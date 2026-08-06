<!-- Header with dynamic stats and badges -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=00B8FF&center=true&vCenter=true&width=500&lines=Aspiring+SRE+%7C+DevOps+%7C+Platform;Homelab+%7C+Observability+%7C+IaC" alt="Typing SVG" />
</p>

<h1 align="center">Stephen Macabulos</h1>
<p align="center">
  <a href="https://portfolio.seekeru.tech"><img src="https://img.shields.io/badge/Portfolio-seekeru.tech-0A0A0A?style=flat-square&logo=githubpages&logoColor=white"></a>
  <a href="https://linkedin.com/in/stephen-macabulos"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white"></a>
  <a href="https://github.com/notseekeru"><img src="https://img.shields.io/badge/GitHub-notseekeru-181717?style=flat-square&logo=github&logoColor=white"></a>
  <a href="mailto:stpmacabulos@gmail.com"><img src="https://img.shields.io/badge/Email-stpmacabulos@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white">
  <img src="https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white">
  <img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white">
  <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white">
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white">
  <img src="https://img.shields.io/badge/ArgoCD-EF7B4D?style=flat-square&logo=argo&logoColor=white">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/NixOS-5277C3?style=flat-square&logo=nixos&logoColor=white">
  <img src="https://img.shields.io/badge/Debian-A81D33?style=flat-square&logo=debian&logoColor=white">
  <img src="https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white">
  <img src="https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square&logo=arch-linux&logoColor=white">
</p>

---

## 🧑‍💻 About Me

To sum it up, I am just a guy very obsessed with tech and infrastructure and that's what keeps me to do what I do.  
I also always eager to learn tech just for learning how it is useful and how does it work.  
Learning, Experimenting, Tinkering is the journey, Simplicity, Clarity and Pragmatism are the end goal.

🎯 Current Goal:

- Experiment on DB Internals such as 3 Way Distributed Database load test, deployment patterns, b-trees, migration, etc.
- Applying High level System Design Concepts on Systems & Applications.

---

<summary>📡 Full infrastructure diagram (July 18, 2026)</summary>
<details>

```mermaid
---
config:
  layout: elk
---
flowchart TB
 subgraph Internet["Public Internet & Edge"]
        Users["End Users"]
        Slack["Slack Channel"]
        CloudflareEdge["Cloudflare Edge (DNS + SSL)"]
        Infisical["Infisical Secret Platform"]
  end

 subgraph GitHub_Platform["🐙 GitHub Platform Ecosystem"]
        subgraph Repositories["Source Repositories (npm Monorepo Workspace)"]
            Git["Infra & Code Repo"]
            App_Monorepo["App Monorepo (Portfolio & Diagram Packages)"]
            GitOps_Repo["GitOps Repo (Manifests)"]
        end

        subgraph CI_Pipeline["GitHub Actions: CI Workflow"]
            CiCheck["Linter / Analysis / Audit"]
        end

        subgraph CD_Pipeline["GitHub Actions: CD Workflow"]
            subgraph Matrix_Jobs["Build & Test Matrix"]
                Build_Local["1. Build Local Image"]
                Trivy["2. Trivy Security Scan"]
                Smoke_Run["3. Run Smoke Container"]
                Push_Multi["4. Push Multi-Arch Image"]

                Build_Local --> Trivy --> Smoke_Run --> Push_Multi
            end

            subgraph Kustomize_Job["Update GitOps Manifests"]
                Clone_GitOps["Clone GitOps Repo"]
                Kustomize_Edit["Kustomize Set Image Tags"]
                Git_Push["Commit & Push to Main"]

                Clone_GitOps --> Kustomize_Edit --> Git_Push
            end

            Trigger -- if CI Success --> Matrix_Jobs
            Matrix_Jobs -- needs --> Kustomize_Job
        end

        GHCR["GitHub Container Registry (GHCR)"]

        Git --> CiCheck
        CI_Pipeline -. Triggers .-> Trigger
        Push_Multi -- Pulls / Pushes --> GHCR
        Git_Push -- Updates --> GitOps_Repo

        App_Monorepo -. Dependabot .-> App_Monorepo
        App_Monorepo --> GitOps_Repo
  end

 subgraph Automation["Automation Control Plane"]
        Makefile["make apply"]
        Ansible["Master Ansible"]
        Terraform["Master Terraform"]
        Kubectl["Kubernetes Control Plane (kubectl)"]
        Kubeconfig["kubeconfig"]
        DynamicInven["Dynamic Inventory"]
  end

 subgraph MainDevices["Management and Orchestration Nodes"]
        MainPC["MainPC"]
        MainLaptop["MainLaptop"]
        Automation
        SSH1["SSH Keys (PC)"]
        SSH2["SSH Keys (Laptop)"]
  end

 subgraph Tailscale["Tailscale Mesh Network"]
        MainDevices
        Pi5
  end

 subgraph Pi5["⚙️ Node - Raspberry Pi 5"]
        subgraph SSHD1["SSHD Hardening"]
            Access["SSH Completed"]
            APerms["No Root Login"]
            AKeys["No Key, No Entry"]
            UFW["Only allow Tailscale Devices"]
            Port22["Only on Port 22"]
            NoIP["No Local IP SSH"]
            F2B["Fail2ban"]
        end

        subgraph Docker["🐳 Docker Containers (Isolated Dev/Test Only)"]
            subgraph ObservabilityStack["Compose - Observability Stack (LGTM + Alloy - Dev/Testing)"]
                Alloy["Grafana Alloy :12345"]
                Prom["Prometheus :9090"]
                Loki["Loki :3100"]
                Tempo["Tempo :3200"]
                Grafana["Grafana Visualization :3030"]
                AManager["AlertManager :9093"]
                DLogs["Docker Logs"]
            end
        end

        subgraph K3s_Cluster["☸️ Local k3s Cluster (Single-Node)"]
            ArgoCD["Helm: ArgoCD Operator"]
            Ingress["Helm: Traefik / Ingress-NGINX"]
            TunnelPod["Cloudflared Tunnel Pod"]

            subgraph Workloads["Namespaces & Pods"]
                subgraph Portfolio_App["Portfolio Stack"]
                    Portfolio_Frontend_Pod["Portfolio Frontend"]
                    Portfolio_Backend_Pod["Portfolio Backend"]
                end

                subgraph Diagram_App["Migrated Diagram Stack"]
                    Frontend2["React/Vite Frontend (Diagram)"]
                    Backend2["Node JS Backend"]
                    Postgres_Pod[("PostgreSQL Pod")]
                end
            end
        end
  end

    Users --> CloudflareEdge
    Makefile --> Terraform & Ansible
    Kubectl --> Kubeconfig
    Terraform --> Kubeconfig & DynamicInven
    Ansible --> DynamicInven
    MainPC --> SSH1
    MainLaptop --> SSH2
    
    F2B --> NoIP
    NoIP --> Port22
    Port22 --> UFW
    UFW --> AKeys
    AKeys --> APerms
    APerms --> Access
    
    Alloy --> DLogs & Prom & Loki & Tempo
    Prom --> Grafana & AManager
    Loki --> Grafana
    Tempo --> Grafana
    SSH1 --> SSHD1
    SSH2 --> SSHD1

    Terraform -- Provisions k3s Resources & Helm Releases --> K3s_Cluster

    GitOps_Repo --> ArgoCD
    ArgoCD --> Workloads
    Workloads -. Self-Heal Control Loop .-> ArgoCD
    Workloads -. Pulls Validated Images .-> GHCR

    CloudflareEdge -- Secure Tunnel --> TunnelPod
    TunnelPod --> Ingress
    Ingress --> Portfolio_Frontend_Pod & Portfolio_Backend_Pod & Frontend2 & Backend2
    Backend2 --> Postgres_Pod
    
    AManager -- Webhook Alerts --> Slack

    Infisical -. Pulls Configuration Secrets .-> Terraform
    Infisical -. Lookup Static Configuration Secrets .-> Ansible
    Terraform -- Creates Secret Resource (via Variables) --> K3s_Cluster

    
```

</details>

---

## 📫 Let's Connect

I'm looking for **internship / entry‑level** opportunities (remote or hybrid).  
or if you just talk in general about tech or even be my friend then you can approach me! (I would be glad to)

- 📧 [stpmacabulos@gmail.com](mailto:stpmacabulos@gmail.com)
- 🔗 [LinkedIn](https://linkedin.com/in/stephen-macabulos)
- 🌐 [Portfolio, Blogs & Infra](https://portfolio.seekeru.tech)
