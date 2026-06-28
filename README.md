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
  <img src="https://img.shields.io/badge/Arch_Linux-1793D1?style=flat-square&logo=arch-linux&logoColor=white">
  <img src="https://img.shields.io/badge/NixOS-5277C3?style=flat-square&logo=nixos&logoColor=white">
  <img src="https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white">
  <img src="https://img.shields.io/badge/Debian-A81D33?style=flat-square&logo=debian&logoColor=white">
</p>

---

## 🧑‍💻 About Me

2nd Year Computer Engineering student from the Philippines, driven by hunger and a will to do the work and learn.
I am very obsessed with tech and infrastructure and that's what keeps me to do what I do.

> Currently my infrastructure repo private for privacy and security reasons

🎯 Current Goal:
- Designing and Building Distributed System by using Kubernetes + Terraform + Cloud Providers
- Experiment on 3 Way Distributed Database load test, indexing, and migration.
- Applying High level System Design Concepts on Systems & Applications
- Studying networking fundamentals to reduce my weakpoints by building my own http engine.

---

<p align="center">
  <img width="41%" src="https://github-readme-stats.vercel.app/api/top-langs/?username=notseekeru&layout=compact&theme=dark&hide_border=true&bg_color=0D1117&title_color=00B8FF&text_color=EEEEEE" />
  <img width="58%" src="https://github-readme-streak-stats.herokuapp.com/?user=notseekeru&theme=dark&hide_border=true&background=0D1117&stroke=00B8FF&ring=00B8FF&fire=00B8FF&currStreakNum=EEEEEE" />
</p>

<details>
<summary>📡 Click to expand full infrastructure diagram (June 13, 2026)</summary>

```mermaid
---
config:
  layout: elk
---
flowchart TB
  subgraph Internet["🌍 Public Internet"]
    Users["End Users"]
    Slack["Slack Channel"]
    CloudflareEdge["Cloudflare Edge"]
  end

  subgraph CI_CD["🔄 GHA CI/CD Pipeline"]
    Git["GitHub Repo CI/CD"]
    ALint["Ansible Lint"]
    Molecule["Molecule Testing"]
    CiCheck["Linter/Formatter/StaticAnalysis/Audit"]
    Trivy["Trivy Security Scan"]
    GHCR["Github Registry"]

    Git --> ALint & CiCheck
    CiCheck --> Trivy
    ALint --> Molecule
    Trivy --> GHCR
  end

  subgraph Tailscale["Tailscale"]
    subgraph MainDevices["🖥️💻 Main Devices"]
      MainPC["MainPC"]
      MainLaptop["MainLaptop"]
      Ansible["Master Ansible"]
      Terraform["Master Terraform"]
      Kubectl["Kubernetes Control Plane"]
      Kubeconfig["kubeconfig"]
      DynamicInven["Dynamic Inventory"]
    end

    Kubectl --> Kubeconfig
    Terraform --> Kubeconfig
    Terraform --> DynamicInven
    Ansible --> DynamicInven

    subgraph MainPC["🖥️ Personal Computer"]
      Ollama["Local Ollama Models"] --> SSH1["SSH Keys"]
    end
    subgraph MainLaptop["💻 Personal Laptop"]
      SSH2["SSH Keys"]
    end

    SSH1 & SSH2 --> SSHD1

    subgraph Pi5["⚙️ Node - Raspberry Pi 5"]
      subgraph SSHD1["🔒 SSHD Configs"]
        F2B["Fail2ban"] --> NoIP["No Local IP SSH"] --> Port22["Only on Port 22"] --> UFW["Only allow Tailscale Devices"] --> AKeys["No Key, No Entry"] --> APerms["No Root Login"] --> Access["SSH Completed"]
      end
      
      subgraph Docker["🐳 Docker Containers"]
        DLogs["Docker Logs"]
        
        subgraph DiagramStack["📊 Compose - Diagram Stack (Observability Experimentation Application)"]
          Frontend2["React/Vite Frontend (Diagram)"]
          subgraph Backend2["Node.js Backend (Diagram)"]
            Nodejs2["Node JS Runtime"]
            OTLPDep["OTLP Metrics HTTP"]
            OTLPDep2["OTLP Spans HTTP"]
          end
          Postgres["Postgres DB :5432"]
          PostgresExporter["Postgres Exporter :9187"]

          Frontend2 -.-> Alloy
          OTLPDep & OTLPDep2 -.-> Alloy
          PostgresExporter --> Postgres
          PostgresExporter -.-> Alloy
        end

        subgraph ObservabilityStack["📊 Compose - Observability Stack (LGTM + Alloy)"]
          Alloy["Grafana Alloy:12345"]
          Prom["Prometheus:9090"]
          Loki["Loki:3100"]
          Tempo["Tempo:3200"]
          Grafana["Grafana Visualization :3030"]
          AManager["AlertManager:9093"]

          Alloy --> DLogs
          Alloy --> Prom
          Alloy --> Loki
          Alloy --> Tempo
          Prom & Loki & Tempo --> Grafana
          Prom --> AManager
          AManager --> Slack
        end
      end
    end
  end

  subgraph DOKS["☸️ DOKS (3-Node Cluster)"]
    ArgoCD["ArgoCD Operator"]
    Ingress["Ingress-Nginx Controller"]
    TunnelPod["Cloudflared Pod"]

    subgraph Workloads["⚙️ Namespaces"]
      Portfolio_Frontend_Pod
      Portfolio_Backend_Pod
    end

    CloudflareEdge --> TunnelPod
    ArgoCD --> Workloads
    TunnelPod --> Ingress
    Ingress --> Portfolio_Frontend_Pod
    Ingress --> Portfolio_Backend_Pod
    Workloads --> GHCR
  end


```

</details>

---

## 📝 Featured Blog Posts

_From my [portfolio blog](https://portfolio.seekeru.tech/blog)_

- 🔥 [**Telemetry Madness**](https://portfolio.seekeru.tech/blog/telemetry-madness) – _I let AI generate my observability stack, then watched it fail silently. Rebuilt from first principles with curl, Alloy, and an MVP OpenTelemetry app._
- ⏱️ [**SRE Steps**](https://portfolio.seekeru.tech/blog/sre-steps) – _Building a reliable kill script to measure real MTTD/MTTR in containerized infrastructure._
- 🛡️ [**Imposter Syndrome**](https://portfolio.seekeru.tech/blog/imposter-syndrome) – _Escaping the blackbox with the fundamentals._

---

## 📫 Let's Connect

I'm looking for **internship / entry‑level** opportunities (remote or hybrid).
or if you just talk in general about tech or even be my peer then you can message me! (I would be glad to)
Let's move forward together!

- 📧 [stpmacabulos@gmail.com](mailto:stpmacabulos@gmail.com)
- 🔗 [LinkedIn](https://linkedin.com/in/stephen-macabulos)
- 🌐 [Portfolio, Blogs & Infra](https://portfolio.seekeru.tech)
