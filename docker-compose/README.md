# **Monitoring stack with Victoria Metrics, Grafana and Loki**

## Includes

**1. VictoriaMetrics:** \
High-performance time series database for storing metrics data.

**2. VMagent (VictoriaMetrics Agent):** \
Scrapes Prometheus targets and pushes metrics to VictoriaMetrics.

**3. Grafana:** \
Popular visualization tool for creating informative dashboards from collected metrics.

**4. Loki:** \
Time series log aggregator for storing and querying logs.

**5. Promtail:** \
Log collection agent that sends logs to Loki.

**6. Node Exporter:** \
Exposes system metrics from the host machine.

**7. Blackbox Exporter:** \
Performs external URL health checks and exposes results as metrics.

## Getting Started

## Prerequisites

*Guide tested on Ubuntu 22.04

**1. Docker and Docker Compose installed on your system.**

```bash
sudo apt update
sudo apt install -y curl wget vim git apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
sudo apt install -y docker-compose
```

Re-login after installation.

**2. Configuration Files:**

Prepare configuration files for each service as needed:

- **.env file (mandatory)**
rename **.env_example** to **.env** and change initial passwords for services.
- prometheus.yaml
- loki.yaml
- promtail.yaml
- blackbox.yaml
Refer to the official documentation of each tool for configuration details.
Environment Variables (Optional):

**3. Clone and Start the Stack:**

- **Clone this repository using Git.**

```bash
cd /opt && sudo git clone https://github.com/plantree-validator/monitoring-stack.git
sudo chown -R $USER /opt/monitoring-stack/
```

- **Run docker-compose up -d to start the stack in detached mode.**

```bash
cd /opt/monitoring-stack/docker-compose/ && docker-compose up -d
```

## Accessing Services

**1. VictoriaMetrics:**

<http://YourInternalIP:8428>

**2. Grafana:**

<http://YourInternalIP:3000>
Login using credentials set in environment variables.

**3. Loki:**

<http://YourInternalIP:3100>

**4. Node Exporter:**

<http://YourInternalIP:9100>

**5. Blackbox Exporter:**

<http://YourInternalIP:9115>

Access health check results as metrics through Grafana or other tools.

## Persistent Data Volumes

The docker-compose configuration defines volumes to persist data:

- vm_data: Stores VictoriaMetrics data.
- vmagent_data: Stores VMagent state information.
- grafana_data: Stores Grafana configuration and user data.
- loki_data: Stores Loki log data.

## Important Notes

Expected usage: \
**Expose services to the Internet via reverse proxy with SSL certificates:** \
Minimal set: \
**1. Grafana:** \
**2. Loki Push API:** \
Should be protected by auth: <https://grafana.com/docs/loki/latest/operations/authentication/> \
Example endpoint for push api: <http://{hostIP}:3100/loki/api/v1/push>

## Reference links

VictoriaMetrics: <https://victoriametrics.com/> \
VMagent: <https://docs.victoriametrics.com/vmagent/> \
Grafana: <https://grafana.com/> \
Loki: <https://grafana.com/docs/loki/latest/> \
Promtail: <https://grafana.com/docs/loki/latest/send-data/promtail/> \
Node Exporter: <https://prometheus.io/docs/guides/node-exporter/> \
Blackbox Exporter: <https://github.com/topics/blackbox-exporter> \
Docker Compose: <https://docs.docker.com/compose/>

## Contributing

Feel free to submit pull requests for improvements or additional features.

I hope this README.md provides a clear and informative guide to setting up and using the Docker Compose monitoring stack.
