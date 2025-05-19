# Zammad-HelpDesk Monitoring CI/CD Stack 

This project automates the deployment of a full-featured **Zammad Helpdesk system** with real-time **monitoring and observability**, using:
- Docker & Docker Compose
- GitHub Actions for CI/CD
- Prometheus + Grafana for monitoring
- SSH-based remote deployment to a VPS

---

## Stack

| Component             | Description |
|---------------        |-------------|
| **Zammad**            | Open-source helpdesk platform |
| **Prometheus**        | Time-series database for monitoring |
| **Grafana**           | Dashboards for visualizing metrics |
| **cAdvisor**          | Container metrics (CPU, memory, network) |
| **node_exporter**     | Host-level metrics |
| **GitHub Actions**    | CI/CD automation with secure deploy |

---

## Directory Structure

```
zammad-auto-deploy/
├── .github/workflows/deploy.yml     # CI/CD pipeline
├── docker-compose.yml               # Zammad stack
├── monitoring/
│   ├── docker-compose.monitoring.yml
│   ├── prometheus.yml
│   └── grafana/
│       ├── datasources/prometheus.yml
│       └── dashboards/
│           ├── dashboard.yaml
│           └── docker-monitoring.json
```

---

## How to Deploy

1. Clone the repo
2. Update the `PRIVATE_KEY`, `USERNAME`, and `HOST` secrets in GitHub
3. Push to `main` → triggers auto deployment to your VPS

```bash
git add .
git commit -m "trigger deploy"
git push origin main
```

The pipeline will:
- SSH into your VPS
- Pull the latest repo
- Run Docker Compose to start/upgrade Zammad + Monitoring

---

##  Monitoring 

- Access Prometheus at: `http://<your-vps-ip>:9090`
- Access Grafana at: `http://<your-vps-ip>:3000` (default: admin/admin)
- Dashboards auto-loaded from `monitoring/grafana/dashboards/`
- You can also import dashboards manually (e.g., Prometheus Node Exporter dashboard ID 193)


## Status

- [x] Automated Zammad deploy via GitHub Actions
- [x] Live container and host monitoring via Prometheus
- [x] Grafana dashboards with auto provisioning
- [x] Secure remote SSH CI/CD

---

## Credits

Built by [Michael Amponsah](https://www.linkedin.com/in/michael-amponsah-4b98329a) to showcase a full DevOps-ready automation pipeline.
