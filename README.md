<!-- Header with dynamic stats and badges -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=00B8FF&center=true&vCenter=true&width=435&lines=Aspiring+SRE+%7C+Platform+Engineer;Homelab+%7C+Observability+%7C+IaC" alt="Typing SVG" />
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
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black">
  <img src="https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white">
</p>

---

## 🧑‍💻 About Me

2nd Year Computer Engineering student from the Philippines, driven by hunger and a will to learn. (sounds corny)
I am very obsessed with tech and infrastructure and that's what keeps me to do what I do.

🎯 Current Goal: Designing and Building Distributed Systems and Learning and applying System Design Concepts

---

## 📈 GitHub Stats

<p align="center">
  <img width="48%" src="https://github-readme-stats.vercel.app/api?username=notseekeru&show_icons=true&theme=dark&hide_border=true&bg_color=0D1117&title_color=00B8FF&icon_color=00B8FF&text_color=EEEEEE" />
  <img width="48%" src="https://github-readme-streak-stats.herokuapp.com/?user=notseekeru&theme=dark&hide_border=true&background=0D1117&stroke=00B8FF&ring=00B8FF&fire=00B8FF&currStreakNum=EEEEEE" />
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=notseekeru&layout=compact&theme=dark&hide_border=true&bg_color=0D1117&title_color=00B8FF&text_color=EEEEEE" />
</p>

---

<details>
<summary>📡 Click to expand full infrastructure diagram (June 13, 2026)</summary>
  
```mermaid
---
config:
  layout: elk
---
flowchart TB
  subgraph PublicEdge["📡 Public Edge Layer"]
    WAF["Cloudflare Edge"]
    CFTunnel["Cloudflare Tunnel"]
  end

  subgraph Internet["🌍 Public Internet"]
    Users["End Users"]
    Slack["Slack Channel"]
  end

  subgraph CI_CD["🔄 GHA CI/CD Pipeline"]
    Git["GitHub Repo CI/CD"]
    ALint["Ansible Lint"]
    Molecule["Molecule Testing"]
    CiCheck["Linter/Formatter/StaticAnalysis"]
    Trivy["Trivy Security Scan"]
    GHCR["Github Registry"]
  end

  subgraph Tailscale["🌐 Tailscale Devices"]
    subgraph MainDevices["🖥️💻 Main Devices"]
      MainPC["MainPC"]
      MainLaptop["MainLaptop"]
      Ansible["Master Ansible"]
      Terraform["Master Terraform"]
    end

    subgraph MainPC["🖥️ Personal Computer"]
      Ollama["Local Ollama Models"] --> SSH1["SSH Keys"]
    end
    subgraph MainLaptop["💻 Personal Laptop"]
      SSH2["SSH Keys"]
    end

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
        end

        subgraph ObservabilityStack["📊 Compose - Observability Stack (LGTM + Alloy)"]
          Alloy["Grafana Alloy:12345"]
          Prom["Prometheus:9090"]
          Loki["Loki:3100"]
          Tempo["Tempo:3200"]
          Grafana["Grafana Visualization :3030"]
          AManager["AlertManager:9093"]
        end
      end
    end

    subgraph DigitalOcean["💧 DigitalOcean Cloud"]
      subgraph Droplet1[" Debian Droplet"]
        Falco["Falco Security"]
        subgraph DODocker["🐳 Docker Compose - Traffic Stack"]
          DONginx["Nginx Reverse Proxy"]
          DOCfD["Cloudflared Container"]
        end

        subgraph AppLayer["💼 Compose - Portfolio Stack (No Telemetry)"]
          Frontend["React/Vite Frontend"]
          Backend["Node.js Backend"]
        end
      end
    end
  end

  Git -- CI Check --> ALint & CiCheck
  CiCheck -- Action --> Trivy
  ALint -- Deploy --> Molecule
  Molecule -- Deploy --> SSHD1
  Trivy -- Build/Push --> GHCR

  Users -- HTTPS --> WAF --> CFTunnel
  CFTunnel -. HTTPS .-> DOCfD
  DOCfD --> DONginx
  DONginx -- HTTP --> Frontend & Backend
  SSH1 & SSH2 -- Tailscale Tunnel --> SSHD1

  Frontend & Backend -- Pull w/Token --> GHCR
  Frontend2 & Nodejs2 -- Pull w/Token --> GHCR

  Alloy -- Scrape Logs --> DLogs
  Alloy -- Remote Write --> Prom
  Alloy -- Loki Push --> Loki
  Alloy -- OTLP --> Tempo
  Prom & Loki & Tempo -- Query --> Grafana
  Prom -- Alerting Rules --> AManager --> Slack

  Frontend2 -. Frontend Logs/Traces .-> Alloy
  OTLPDep & OTLPDep2 -. OTLP Metrics & Spans .-> Alloy
  PostgresExporter -- Scrapes Metrics --> Postgres
  PostgresExporter -. Metrics :9187 .-> Alloy
</details>
```
---

## 📝 Featured Blog Posts

*From my [portfolio blog](https://portfolio.seekeru.tech/blog)*

- 🔥 [**Telemetry Madness**](https://portfolio.seekeru.tech/blog/telemetry-madness) – *I let AI generate my observability stack, then watched it fail silently. Rebuilt from first principles with curl, Alloy, and an MVP OpenTelemetry app.*  
- ⏱️ [**SRE Steps**](https://portfolio.seekeru.tech/blog/sre-steps) – *Building a reliable kill script to measure real MTTD/MTTR in containerized infrastructure.*  
- 🛡️ [**Imposter Syndrome**](https://portfolio.seekeru.tech/blog/imposter-syndrome) – *Escaping the blackbox.*

---

## 🚀 Featured Projects

<table width="100%">
  <tr>
    <td width="100%" valign="top">
      <h3>📦 Ansible Automation</h3>
      <p>CIS Level‑1 hardening, Tailscale bootstrap, Molecule tests, idempotent roles.</p>
      <p><code>ansible-lint</code> <code>Jinja</code> <code>Makefile</code></p>
      <a href="https://github.com/notseekeru/ansible"><img src="https://img.shields.io/badge/Repository-181717?style=flat-square&logo=github&logoColor=white"></a>
    </td>
  </tr>
  <tr>
    <td width="100%" valign="top">
      <h3>🏗️ Terraform IaC</h3>
      <p>DigitalOcean droplets + SSH keys + dynamic inventory for Ansible.</p>
      <p><code>HCL</code> <code>Makefile</code> <code>Go Template</code></p>
      <a href="https://github.com/notseekeru/terraform"><img src="https://img.shields.io/badge/Repository-181717?style=flat-square&logo=github&logoColor=white"></a>
    </td>
  </tr>
  <tr>
    <td width="100%" valign="top">
      <h3>📊 Diagram Website + Observability</h3>
      <p>CRUD Mermaid diagrams, chaos scripts, LGTM+Alloy pipeline, Traffic Simulation.</p>
      <p><code>TypeScript</code> <code>React</code> <code>Node.js</code></p>
      <a href="https://github.com/notseekeru/diagram_website"><img src="https://img.shields.io/badge/Repository-181717?style=flat-square&logo=github&logoColor=white"></a>
    </td>
  </tr>
</table>

---

## 📫 Let's Connect

I'm looking for **internship / entry‑level** opportunities (remote or hybrid).
or if you just talk in general about tech or even be my peer then you can message me! (I would be glad to)
Let's move forward together!

- 📧 [stpmacabulos@gmail.com](mailto:stpmacabulos@gmail.com)  
- 🔗 [LinkedIn](https://linkedin.com/in/stephen-macabulos)  
- 🌐 [Portfolio, Blogs & Infra](https://portfolio.seekeru.tech)  

---

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=notseekeru&label=Profile%20Views&color=00B8FF&style=flat-square" />
</p>
