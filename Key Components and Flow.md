## Key Components and Flow


This project implements a Linux server monitoring solution using Prometheus, Grafana, and Node Exporter to provide real-time visibility into system performance and resource utilization.

### 1. Linux Server

The Linux server acts as the monitored target machine. It generates system metrics such as CPU usage, memory consumption, disk utilization, network activity, and system load.

### 2. Node Exporter

Node Exporter is installed on the Linux server to collect hardware and operating system metrics. It exposes these metrics through an HTTP endpoint that can be accessed by Prometheus.

### 3. Prometheus

Prometheus is configured to periodically scrape metrics from Node Exporter. It stores the collected data in a time-series database and enables efficient querying of historical and real-time system metrics.

### 4. Grafana

Grafana is connected to Prometheus as a data source. It retrieves metrics from Prometheus and presents them through interactive dashboards, graphs, gauges, and panels for easy monitoring and analysis.

### Monitoring Flow

Linux Server
→ Node Exporter collects system metrics
→ Prometheus scrapes and stores metrics
→ Grafana visualizes metrics through dashboards
→ Administrator monitors system health and performance

### Metrics Monitored

* CPU Utilization
* Memory Usage
* Disk Space Usage
* Network Traffic
* System Load Average
* Server Uptime
* Running Processes
* Filesystem Usage

### Benefits

* Real-time infrastructure monitoring
* Centralized performance visualization
* Faster issue detection and troubleshooting
* Historical performance analysis
* Improved system reliability and observability

This project demonstrates practical DevOps skills in Linux administration, monitoring, observability, and infrastructure management using industry-standard open-source tools.
