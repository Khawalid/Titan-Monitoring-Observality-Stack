# 🚀 Prometheus + Grafana Monitoring Stack with Alerting & Slack Integration

# 📌 Overview

This project demonstrates a complete end-to-end Monitoring and Observability stack built using Prometheus, Grafana, and Slack integration. It showcases how infrastructure metrics and application metrics can be collected, queried using PromQL, visualized through dashboards, and converted into actionable alerts.

The system monitors:

- 🖥️ Server health and availability
- 🧠 Memory utilization
- 💽 Disk usage
- ⚙️ CPU load
- 🌐 Application HTTP request metrics
- 🚨 Real-time alert notifications via Slack

The implementation reflects a real-world DevOps monitoring workflow where metrics are scraped from exporters, stored in Prometheus, visualized in Grafana, and alerts are delivered instantly to collaboration platforms.

This project simulates a production-style monitoring setup suitable for cloud-based Linux servers and modern application environments.

---

# 🏗️ 1. System Architecture

![Architecture](./screenshots/Architecture%20Diagram..png)

The architecture follows a distributed model to prevent bottlenecks and ensure scalability. Data flows from managed agents on the Application Server to centralized databases for metrics and logs.

## 📡 Infrastructure Port Mapping

| Service       | Port  | Description                        |
| ------------- | ----- | ---------------------------------- |
| Grafana       | 3000  | Unified UI for Dashboards & Alerts |
| Prometheus    | 1990  | Time-series Metrics Database       |
| Loki          | 3100  | High-efficiency Log Aggregation    |
| Node Exporter | 9100  | Hardware & OS Metric Exposure      |
| Titan App     | 5000  | Python Flask Web Application       |
| Grafana Alloy | 12345 | Unified Observability Agent        |

---

# 🛠️ 2. The Observability Stack

- **Metrics Management:** Prometheus uses a "Pull" (Scraping) model to collect time-series data from exposed endpoints.

- **Log Management:** Grafana Loki serves as a cost-effective log aggregation system, receiving logs pushed from agents.

- **Visualization:** Grafana acts as the unified frontend, connecting to Prometheus and Loki to create interactive dashboards.

- **Unified Agent:** Grafana Alloy handles metrics, logs, and traces in a single binary, replacing legacy agents like Promtail.

- **Infrastructure:** Hosted on AWS EC2 (Ubuntu 24.04) instances, utilizing t2.micro types for development.

---

# ⚙️ 3. Automated Deployment

The environment is provisioned using automated Bash scripts to ensure consistency and minimize configuration errors.

- **Grafana Setup:** grafana-setup.sh
- **Prometheus Setup:** prometheus-setup.sh
- **Loki Setup:** lokisetup.sh
- **Application Node:** webnode_setup.sh

---

# 🔍 4. Data Exploration & PromQL

This project leverages PromQL (Prometheus Query Language) to extract actionable insights from raw telemetry.

- **Instant Vectors:** up == 1
- **Range Vectors:** up[5m]
- **Resource Arithmetic:** Memory & disk percentage calculations
- **Rate Analysis:** rate(http_requests_total[1m])

---

# 📈 5. Dashboards & Visualizations

- **Time Series Panels:** CPU & traffic trends
- **Gauge Panels:** Memory & disk visualization
- **Dynamic Variables:** Interactive endpoint filtering

---

# 🚨 6. Alerting & Incident Management

- **Slack Contact Point:** #alerts-prods webhook integration
- **Threshold Rules:** Root disk usage > 65%
- **Notification Policies:** Managed repeat intervals

---

# 📷 7. Project Gallery (37-Step Workflow)

## 🏗️ Phase 1: Infrastructure & Service Deployment

### Snapshot 1: Grafana Installation Automation

![snapshots](./screenshots/1.png)
Executing `grafana-setup.sh` to automate Grafana installation and service enablement.

### Snapshot 2: Initial Grafana UI Access

![snapshots](./screenshots/2.png)
Accessing Grafana on port 3000 for the first time after successful deployment.

### Snapshot 3: Grafana Admin Login & Dashboard Home

![snapshots](./screenshots/3.png)
Successful administrative login confirming Grafana service health.

### Snapshot 4: Prometheus Systemd Deployment

![snapshots](./screenshots/4.png)
Running `prometheus-setup.sh` to install Prometheus as a managed system service.

### Snapshot 5: Prometheus Self-Scraping Verification

![snapshots](./screenshots/5.png)
Validating that Prometheus is scraping its internal metrics successfully.

### Snapshot 6: EC2 Instance Overview

![snapshots](./screenshots/6.png)
Displaying provisioned Prometheus and Grafana EC2 instances.

### Snapshot 7: Loki Service Status Confirmation

![snapshots](./screenshots/7.png)
Terminal confirmation that the Loki service is active and running.

### Snapshot 8: Loki API Readiness Check

![snapshots](./screenshots/8.png)
Verification that the Loki API endpoint is responding as "ready" on port 3100.

### Snapshot 9: Application Node Automation

![snapshots](./screenshots/9.png)
Executing `webnode_setup.sh` to configure the Titan application server.

---

## 📡 Phase 2: Application Monitoring & Data Flow

### Snapshot 10: Titan Application Live

![snapshots](./screenshots/10.png)
Python Flask Titan application running successfully on port 5000.

### Snapshot 11: Payment Endpoint Validation

![snapshots](./screenshots/11.png)
Testing the `/payment` endpoint to simulate application traffic.

### Snapshot 12: Application Metrics Exposure

![snapshots](./screenshots/12.png)
Viewing internal metrics exposed by the Flask application.

### Snapshot 13: Node Exporter Metrics Endpoint

![snapshots](./screenshots/13.png)
System-level hardware and OS metrics exposed on port 9100.

### Snapshot 14: Active Load Simulation

![snapshots](./screenshots/14.png)
Using `top` to verify active load generation scripts consuming CPU.

### Snapshot 15: Log File Generation

![snapshots](./screenshots/15.png)
Confirming application logs are being generated in `/var/log/titan/`.

---

## 🔍 Phase 3: PromQL Mastery & Target Discovery

### Snapshot 16: Healthy Scrape Targets

![snapshots](./screenshots/16.png)
Prometheus UI showing all configured scrape targets as healthy.

### Snapshot 17: Node Status Check (up Metric)

![snapshots](./screenshots/17.png)
Executing `up` query to validate instance availability.

### Snapshot 18: Historical Query Using Range Vector

![snapshots](./screenshots/18.png)
Retrieving historical status using `up[5m]`.

### Snapshot 19: Counting Active Targets

![snapshots](./screenshots/19.png)
Using `count(up)` to calculate total monitored targets.

### Snapshot 20: Scalar Conversion

![snapshots](./screenshots/20.png)
Applying `scalar()` to convert vector results into numerical output.

### Snapshot 21: Total System Memory Query

![snapshots](./screenshots/21.png)
Querying total system memory in bytes.

### Snapshot 22: Used Memory Calculation

![snapshots](./screenshots/22.png)
Calculating used memory through metric subtraction.

### Snapshot 23: Root Filesystem Utilization

![snapshots](./screenshots/23.png)
Computing available root filesystem percentage.

### Snapshot 24: Filtering Active Instances

![snapshots](./screenshots/24.png)
Filtering active nodes using `up == 1`.

### Snapshot 25: High Load Detection

![snapshots](./screenshots/25.png)
Identifying nodes experiencing high load averages.

### Snapshot 26: Combined Condition Filtering

![snapshots](./screenshots/26.png)
Finding nodes that are both operational and under load.

### Snapshot 27: Offset Query for Historical Memory

![snapshots](./screenshots/27.png)
Using `offset 5m` to analyze previous memory states.

### Snapshot 28: HTTP Request Counter

![snapshots](./screenshots/28.png)
Tracking `http_requests_total` metric for Titan application.

### Snapshot 29: Request Rate Analysis

![snapshots](./screenshots/29.png)
Calculating per-second request rate using `rate()`.

### Snapshot 30: Metric Aggregation by Labels

![snapshots](./screenshots/30.png)
Summing metrics grouped by specific job labels.

---

## 🚨 Phase 4: Visualization & Alerting Integration

### Snapshot 31: Prometheus Data Source Connection

![snapshots](./screenshots/31.png)
Connecting Prometheus to Grafana using private IP configuration.

### Snapshot 32: Grafana Explore Live Query

![snapshots](./screenshots/32.png)
Testing real-time metric queries in Grafana Explore.

### Snapshot 33: Slack Webhook Configuration

![snapshots](./screenshots/33.png)
Establishing Slack webhook integration for alert notifications.

### Snapshot 34: Time Series Panel Creation

![snapshots](./screenshots/34.png)
Building performance monitoring panels using Time Series visualization.

### Snapshot 35: Bar Chart Visualization

![snapshots](./screenshots/35.png)
Using bar charts to compare categorical infrastructure metrics.

### Snapshot 36: Memory Gauge Panel

![snapshots](./screenshots/36.png)
Creating a Gauge panel to visualize available system memory.

### Snapshot 37: Alert Threshold Configuration

![snapshots](./screenshots/37.png)
Defining color thresholds and alert triggers for critical metrics.

---

# 🧪 8. Testing & Simulation

- **System Load:** load.sh CPU spike testing
- **Traffic Simulation:** curl-based endpoint stress
- **Log Generation:** Fake logs in /var/log/titan/

---

# ⚖️ License

This project is licensed under the MIT License.
