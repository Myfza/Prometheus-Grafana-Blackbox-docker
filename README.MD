# 🔍 Prometheus + Grafana + Blackbox + Lighthouse Monitoring Stack

A **drop-in monitoring stack** built with Docker Compose that includes:

- 📈 **Host metrics** via Node Exporter  
- 🔧 **Redis metrics** via Redis Exporter  
- 🌐 **HTTP(S) availability monitoring** via Blackbox Exporter  
- ⚡ **Web performance audits** via Lighthouse (on-demand)  
- 📊 Pre-provisioned **Grafana dashboards**  
- 📓 Jupyter Notebook to visualize data

---

## 🚀 Quick Start

```bash
git clone https://github.com/your-username/monitoring-stack
cd monitoring-stack
docker compose up -d
```

| Service         | URL                      | Credentials      |
|-----------------|--------------------------|------------------|
| Prometheus UI   | http://localhost:9090    | -                |
| Grafana         | http://localhost:3000    | admin / admin123 |
| Blackbox Exporter | http://localhost:9115 | -                |

> ⚠️ **Grafana is pre-provisioned.** If you change any dashboard, export it to JSON and commit the file to keep it version-controlled.

---

## 📁 Folder Structure

```
.
├── README.md
├── docker-compose.yml
├── prometheus.yml
├── blackbox.yml
├── rules/                   # Prometheus alerting/recording rules
├── grafana/
│   └── provisioning/        # Auto-loaded dashboards & datasources
└── monitoring-dashboard.ipynb
```

---

## 🧠 Configuration Notes

### 🔧 Prometheus

To add or modify targets, edit `prometheus.yml` and adjust `job_name` and `static_configs`.

Apply changes:
```bash
docker compose kill -s SIGHUP prometheus  # hot-reload
# or
docker compose restart prometheus         # full restart
```

### 📢 Alerting Rules

Add `.yml` files in `rules/`. Prometheus will load them via the `rule_files` directive.

---

## ⚡ Lighthouse Reports (Performance Audit)

Run ad-hoc audits:

```bash
docker compose run --rm lighthouse   lighthouse https://example.com --output=json --output-path=/tmp/report.json
```

To persist reports, mount volume in `docker-compose.yml`:

```yaml
volumes:
  - ./reports:/tmp
```

---

## 📊 Jupyter Notebook Dashboard

Visualize live metrics in the included notebook:

Open with JupyterLab or VS Code:

```bash
jupyter lab monitoring-dashboard.ipynb
```

### 🧪 Install Python dependencies once:

```bash
pip install prometheus-api-client pandas matplotlib seaborn jupyter
```

---

## 🧹 Tear Down

```bash
docker compose down -v  # Also removes named volumes
```

---

## 🧑‍💻 Author

**Muhammad Yusuf Aditiya**  
🔗 [LinkedIn](https://www.linkedin.com/in/muhammadyusufaditiya)  
💻 Open-source enthusiast | Full Stack Automation & Industrial Tech Developer  

---