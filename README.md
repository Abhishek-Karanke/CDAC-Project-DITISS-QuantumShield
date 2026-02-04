# QuantumShield – Secure DevSecOps Pipeline

## 📌 Project Overview

**QuantumShield** is an end‑to‑end **Secure DevSecOps pipeline** designed to demonstrate how security, automation, GitOps, and observability can be integrated seamlessly into modern cloud‑native application delivery.

The project covers the complete lifecycle — from **code commit** to **secure deployment on Kubernetes**, with **continuous security scanning**, **quality gates**, **GitOps‑based CD**, and **real‑time monitoring**.

---

## 🏗️ High‑Level Architecture

![WhatsApp Image 2026-01-28 at 16 47 21](https://github.com/user-attachments/assets/f4bcdd9c-b1d4-46eb-b6f0-59e5ab8fbbe8)

The architecture is divided into **four security zones**:

### 🔹 Zone 1: Source & Registry (External)

* Developer workstation
* GitHub repository (application code + Kubernetes manifests)
* Docker Hub (container image registry)

### 🔹 Zone 2: Continuous Integration (CI Network)

* Jenkins Master (pipeline orchestration)
* Jenkins Agent (build & scan)
* Integrated tools:

  * Docker
  * SonarQube (static code analysis)
  * Trivy (container vulnerability scanning)

### 🔹 Zone 3: Kubernetes Cluster (Production)

* Kubernetes Control Plane (API Server, Scheduler, etcd)
* Worker Node (application workloads)
* Argo CD (GitOps continuous delivery)
* Flask application deployed as pods & service

### 🔹 Zone 4: Security & Monitoring (DMZ)

* Prometheus (metrics scraping)
* Grafana (dashboards & visualization)
* Node Exporter (host‑level metrics)

---

## 📂 GitHub Repository Structure

```
.
├── argocd/                 # Argo CD application manifests
├── k8s-manifest/           # Kubernetes deployment & service YAMLs
├── static/                 # Static files for Flask app
├── templates/              # HTML templates (login, upload UI)
├── uploads/                # Uploaded files directory
├── Jenkinsfile             # CI/CD pipeline definition
├── dockerfile              # Docker image build instructions
├── requirements.txt        # Python dependencies
├── app.py                  # Flask application source code
├── app.db                  # SQLite database
├── README.md               # Project documentation
```

---

## 🔄 CI/CD Pipeline Flow (Stage‑wise)

### 1️⃣ Code Commit

* Developer pushes code to GitHub
* Webhook triggers Jenkins pipeline automatically

### 2️⃣ Jenkins CI Pipeline Stages

<img width="1919" height="1079" alt="Screenshot 2026-02-03 104933" src="https://github.com/user-attachments/assets/673ab611-0a13-4681-9144-8410d6fd205d" />

* **Checkout SCM** – Pull source code
* **SonarQube Analysis** – Static code analysis
* **Quality Gate** – Pipeline halts if gate fails
* **Setup Python Environment**
* **Lint Code** – Code style checks
* **Run Unit Tests**
* **Health Check**
* **Build Docker Image**
* **Trivy Image Scan** – CVE & misconfiguration scan
* **Docker Login & Push** – Push only secure images
* **Commit K8s Manifests** – Update image tag for GitOps

✔️ Failed stages stop the pipeline automatically

---

## 🔐 Security Implementation

<img width="1920" height="1080" alt="Screenshot (34)" src="https://github.com/user-attachments/assets/80a676cb-132b-4400-963d-4c6f6607b2e9" />


* **Shift‑Left Security** using SonarQube
* **Container Security** using Trivy
* **Quality Gates** enforce minimum standards
* **No insecure images** pushed to registry
* **GitOps ensures immutable deployments**

---

## 🚀 Continuous Delivery with Argo CD

<img width="1919" height="1079" alt="Screenshot 2026-02-03 105445" src="https://github.com/user-attachments/assets/536b5e15-1abc-4f14-a327-4c448b0c6ffa" />

* Argo CD watches GitHub manifests
* Auto‑sync enabled
* On image tag update:

  * Old ReplicaSet replaced
  * New pods created automatically
* Deployment status visible in Argo CD UI

---

## 📊 Monitoring & Observability

### Metrics Collection

* Node Exporter installed on:

  * Jenkins Master
  * Kubernetes Master
  * Kubernetes Worker

### Prometheus

* Scrapes metrics from Node Exporter
* Stores time‑series data

### Grafana Dashboards

<img width="1524" height="881" alt="Screenshot 2026-02-03 112226" src="https://github.com/user-attachments/assets/ed9f71a6-9b01-4855-b62e-e8ca068f83d0" /><img width="1918" height="982" alt="Screenshot 2026-02-03 112323" src="https://github.com/user-attachments/assets/fa12d731-f918-4673-9eb3-40a444ecc94c" />

* CPU, Memory, Disk, Network
* Per‑node monitoring
* Real‑time visualization

---

## 🌐 Application Overview

<img width="1905" height="1052" alt="Screenshot 2026-02-03 105510" src="https://github.com/user-attachments/assets/4acc2342-bbf5-43e9-a922-a0977fb8092b" /><img width="1914" height="1069" alt="Screenshot 2026-02-03 105609" src="https://github.com/user-attachments/assets/63de925f-9a4f-44d1-a8c1-c38baeb20c52" />


* Flask‑based secure web application
* Features:

  * Login authentication
  * Secure file upload
  * UI deployed inside Kubernetes
* Exposed via Kubernetes Service (NodePort)

---

## 🧠 Challenges Faced & Solutions

| Challenge                                | Solution                             |
| ---------------------------------------- | ------------------------------------ |
| Pipeline failures due to vulnerabilities | Enforced Trivy severity thresholds   |
| Argo CD sync issues                      | Corrected manifest paths & auto‑sync |
| Resource constraints                     | Tuned VM CPU/RAM                     |
| Monitoring gaps                          | Added Node Exporter on all nodes     |

---

## 🧑‍💻 Author

**Abhishek Karanke**
CDAC‑DITISS | DevSecOps Final Project

---

## 📌 Key Takeaways

* Security integrated at every stage
* Fully automated CI/CD pipeline
* GitOps‑based production deployments
* Centralized monitoring & observability

---

✅ *This project demonstrates real‑world DevSecOps practices aligned with industry standards.*
