# Setting Up Monitoring Stack on Ubuntu 22.04

This guide helps you set up a monitoring stack on Ubuntu 22.04 using Docker, Docker Compose, VictoriaMetrics, Grafana, Loki, and Promtail.

## Step 1: Install Docker

```bash
sudo apt update
sudo apt install -y curl wget vim git apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```


## Step 2: Add User to Docker Group and install Docker Compose

```bash
sudo usermod -aG docker $USER
sudo apt install -y docker-compose
```
## Step 3: Relogin to refresh user's privileges 

## Step 4: Create Necessary Directories for Monitoring Stack

```bash
mkdir -p /opt/monitoring-stack/victoriametrics-data /opt/monitoring-stack/victoriametrics-data /opt/monitoring-stack/victoriametrics-data/grafana-data loki-data /opt/monitoring-stack/victoriametrics-data/promtail-config
```

## Step 5: Clone repo

```bash
git clone https://github.com/plantree-validator/monitoring-stack.git /opt
```

## Step 6: Run docker-compose stack

```bash
cd /opt/monitoring-stack && docker-compose up -d
```