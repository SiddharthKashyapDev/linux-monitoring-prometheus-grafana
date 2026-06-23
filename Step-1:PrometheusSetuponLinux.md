## Prometheus Environment Setup

### Update System and Install Dependencies

```bash
sudo apt update && sudo apt install -y wget tar
```

### Download and Install Prometheus

```bash
cd /opt

sudo wget https://github.com/prometheus/prometheus/releases/download/v3.7.1/prometheus-3.7.1.linux-amd64.tar.gz

sudo tar -xvf prometheus-3.7.1.linux-amd64.tar.gz

sudo mv prometheus-3.7.1.linux-amd64 prometheus
```

### Create Prometheus User

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```

### Move Binaries and Create Required Directories

```bash
sudo mv /opt/prometheus/prometheus /usr/local/bin/

sudo mv /opt/prometheus/promtool /usr/local/bin/

sudo mkdir -p /etc/prometheus

sudo mkdir -p /var/lib/prometheus
```

### Set Permissions

```bash
sudo chown prometheus:prometheus /usr/local/bin/prometheus

sudo chown prometheus:prometheus /usr/local/bin/promtool

sudo chown -R prometheus:prometheus /etc/prometheus

sudo chown -R prometheus:prometheus /var/lib/prometheus
```

### Configure Prometheus

Create the configuration file:

```bash
sudo nano /etc/prometheus/prometheus.yml
```

Add the following configuration:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'linux_node_exporter'
    static_configs:
      - targets: ['192.168.126.131:9100']
```

**Note:** Replace `192.168.126.131` with your Linux VM IP address if it changes.

### Create Prometheus Systemd Service

Create a service file:

```bash
sudo nano /etc/systemd/system/prometheus.service
```

Add the following content:

```ini
[Unit]
Description=Prometheus Monitoring Service
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple

ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.console.templates=/opt/prometheus/consoles \
  --web.console.libraries=/opt/prometheus/console_libraries

Restart=always

[Install]
WantedBy=multi-user.target
```

### Enable and Start Prometheus

```bash
sudo systemctl daemon-reload

sudo systemctl enable prometheus

sudo systemctl start prometheus

sudo systemctl status prometheus
```

### Verify Installation

Open your browser and visit:

```text
http://localhost:9090
```

### Check Targets

Navigate to:

```text
Status → Targets
```

Verify that:

* Prometheus target is UP
* Linux Node Exporter target is UP

### Result

Prometheus is now successfully configured to collect and store real-time metrics from the Linux server through Node Exporter. These metrics can be visualized using Grafana dashboards for infrastructure monitoring and performance analysis.
