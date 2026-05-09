# 🚀 Kestra Website Monitoring Platform

A production-style workflow orchestration and website monitoring platform built using Kestra, Docker, PostgreSQL, and AWS EC2.

This project demonstrates how modern DevOps and Platform Engineering teams can automate health checks, monitor infrastructure endpoints, orchestrate workflows, and build scalable monitoring systems using Kestra.

---

# 📌 Project Overview

This platform continuously monitors multiple websites and APIs on a schedule using Kestra workflows.

The workflow:

* Runs automatically every 5 minutes
* Sends HTTP health-check requests
* Logs response status for each monitored endpoint
* Uses workflow orchestration concepts like looping, scheduling, variables, and task outputs
* Runs fully containerized using Docker Compose
* Uses PostgreSQL as Kestra backend database
* Hosted on AWS EC2

---

# 🏗️ Architecture

```text
                +----------------+
                |   Kestra UI    |
                +--------+-------+
                         |
                         v
                +----------------+
                | Kestra Engine  |
                | Workflow Core  |
                +--------+-------+
                         |
        +-------------------------------+
        |                               |
        v                               v
+---------------+              +----------------+
| HTTP Requests |              | PostgreSQL DB |
| Website Checks|              | Metadata Store|
+---------------+              +----------------+
                         |
                         v
                +----------------+
                | AWS EC2 Server |
                +----------------+
```

---

# ⚙️ Tech Stack

| Technology     | Purpose                    |
| -------------- | -------------------------- |
| Kestra         | Workflow orchestration     |
| Docker         | Containerization           |
| Docker Compose | Multi-container management |
| PostgreSQL     | Kestra metadata database   |
| AWS EC2        | Cloud hosting              |
| YAML           | Workflow definitions       |
| Linux          | Server environment         |

---

# ✨ Features

## ✅ Automated Workflow Scheduling

Runs monitoring workflows automatically every 5 minutes using cron triggers.

## ✅ Website Health Monitoring

Checks availability and response status of:

* Google
* GitHub
* Kestra
* Amazon

## ✅ Workflow Orchestration

Uses Kestra flow orchestration concepts:

* Triggers
* Variables
* ForEach loops
* Task outputs
* Logging
* HTTP tasks

## ✅ Scalable Monitoring Logic

Easily extend monitoring to:

* APIs
* Kubernetes ingress
* Internal applications
* Load balancers
* Health endpoints

## ✅ Containerized Deployment

Entire platform runs in Docker containers for portability and scalability.

## ✅ Cloud Deployment

Hosted on AWS EC2 for real-world production-style deployment.

---

# 📂 Project Structure

```text
kestra-monitoring-project/
│
├── docker-compose.yml
├── flows/
│   └── website_monitor.yml
├── screenshots/
├── README.md
└── .gitignore
```

---

# 📜 Workflow Definition

```yaml
id: website_monitor
namespace: dev.monitoring

description: Monitor websites every 5 minutes

triggers:
  - id: every_5_minutes
    type: io.kestra.plugin.core.trigger.Schedule
    cron: "*/5 * * * *"

variables:
  websites:
    - https://google.com
    - https://github.com
    - https://kestra.io
    - https://amazon.com

tasks:

  - id: monitor_sites
    type: io.kestra.plugin.core.flow.ForEach

    values: "{{ vars.websites }}"

    tasks:

      - id: check_website
        type: io.kestra.plugin.core.http.Request

        uri: "{{ taskrun.value }}"
        method: GET

      - id: log_result
        type: io.kestra.plugin.core.log.Log

        message: |
          Website: {{ taskrun.value }}
```

---

# 🐳 Docker Compose Configuration

```yaml
services:
  postgres:
    image: postgres:15
    container_name: kestra_postgres
    environment:
      POSTGRES_DB: kestra
      POSTGRES_USER: kestra
      POSTGRES_PASSWORD: kestra
    volumes:
      - postgres-data:/var/lib/postgresql/data

  kestra:
    image: kestra/kestra:latest
    container_name: kestra
    ports:
      - "8080:8080"
    environment:
      KESTRA_CONFIGURATION: |
        datasources:
          postgres:
            url: jdbc:postgresql://postgres:5432/kestra
            driverClassName: org.postgresql.Driver
            username: kestra
            password: kestra
    depends_on:
      - postgres

volumes:
  postgres-data:
```

---

# 🚀 Deployment Steps

## 1️⃣ Launch AWS EC2

* Ubuntu Server
* Open ports:

  * 22
  * 8080
  * 80
  * 443

---

## 2️⃣ Install Docker

```bash
sudo apt update
sudo apt install docker.io docker-compose-plugin -y
sudo systemctl enable docker
sudo systemctl start docker
```

---

## 3️⃣ Clone Repository

```bash
git clone <your-repo-url>
cd kestra-monitoring-project
```

---

## 4️⃣ Start Platform

```bash
docker compose up -d
```

---

## 5️⃣ Access Kestra UI

```text
http://<EC2-PUBLIC-IP>:8080
```

---

# 📸 Screenshots

## Kestra Dashboard

*Add screenshot here*

## Workflow Execution

*Add screenshot here*

## Logs & Monitoring

*Add screenshot here*

---

# 🧠 Key DevOps Concepts Demonstrated

* Workflow orchestration
* Infrastructure automation
* Containerized deployment
* Cloud hosting
* Health monitoring
* Scheduling automation
* YAML-based Infrastructure as Code
* Platform engineering concepts
* Observability workflows
* Automated execution pipelines

---

# 🔥 Challenges Solved During Implementation

During implementation, several production-like issues were identified and resolved:

* PostgreSQL migration compatibility issues
* Docker container startup failures
* EC2 resource limitations
* Port accessibility and networking
* Workflow debugging in Kestra
* Task output handling and expression debugging
* Workflow scheduling and orchestration troubleshooting

This project helped strengthen practical troubleshooting and DevOps debugging skills.

---

# 📈 Future Enhancements

Planned improvements:

* Prometheus integration
* Grafana dashboards
* Slack/Email alerts
* SSL certificate monitoring
* Kubernetes cluster monitoring
* Auto-remediation workflows
* Incident management automation
* Daily uptime reports
* API latency tracking
* Infrastructure cost monitoring

---

# 👨‍💻 About This Project

This project was built to gain hands-on experience with workflow orchestration, DevOps automation, and cloud-native monitoring systems.

It showcases practical implementation skills around:

* DevOps Engineering
* Platform Engineering
* Site Reliability Engineering (SRE)
* Infrastructure Automation
* Workflow Orchestration

---

# ⭐ If You Found This Useful

Feel free to star the repository and connect with me on LinkedIn.

---

# 📬 Connect

LinkedIn: *Add your LinkedIn URL here*

GitHub: *Add your GitHub URL here*
