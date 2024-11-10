# ML Model API Observability Stack

This project sets up a full observability stack to keep an eye on and analyze your Machine Learning (ML) Model API. Using Elasticsearch, Kibana, Logstash, Filebeat, Metricbeat, and Heartbeat, it makes it easy to collect, explore, and visualize logs and metrics. Everything runs with Docker Compose to manage all the containerized services smoothly, based on the [Elastic Stack (ELK) on Docker](https://github.com/deviantony/docker-elk). It’s designed to monitor and support the [Machine Learning API Environment](https://github.com/thiagofmiranda/machine-learning-api), giving you better insights and performance tracking.

## Table of Contents

- [Overview](#overview)
- [Services](#services)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Volumes and Networks](#volumes-and-networks)
- [Troubleshooting](#troubleshooting)

## Overview

This observability stack monitors the performance, health, and behavior of a Machine Learning API, offering centralized logging, metric collection, heartbeat monitoring, and robust visualization.

## Services

- **Elasticsearch:** Serves as the core for indexing and storing logs and metrics.
- **Logstash:** Collects, parses, and transforms data before forwarding it to Elasticsearch.
- **Kibana:** Offers a web interface to visualize data from Elasticsearch.
- **Filebeat:** Collects and ships log files, such as Nginx logs, to Logstash or Elasticsearch.
- **Metricbeat:** Gathers metrics from systems and services.
- **Heartbeat:** Tracks uptime and availability of services.

## Getting Started

1. Clone and Run the [Machine Learning API repository](https://github.com/thiagofmiranda/machine-learning-api).
2. Clone this repository.
3. Copy the `.env.example` file to `.env` and configure your environment variables.
4. Build and start the stack:

The `setup` service initializes users, roles, and passwords in Elasticsearch during the initial startup:

```bash
docker compose up setup
```

Running the stack:
```bash
docker compose up
```

Give Kibana about a minute to initialize, then access the Kibana web UI by opening [http://localhost:5601](http://localhost:5601) in a web browser and use the following (default) credentials to log in:

- user: elastic
- password: <YOUR_PASSWORD>

## Configuration

You can customize configurations for each service within the corresponding directories:
- Elasticsearch: `./elasticsearch/config/elasticsearch.yml`
- Logstash: `./logstash/config/logstash.yml`
- Kibana: `./kibana/config/kibana.yml`
- Filebeat, Metricbeat, Heartbeat configurations are found in `./extensions/`.

### Environment Variables

The `.env` file defines key environment variables, such as passwords for internal users and configurations.

## Volumes and Networks

- **Volumes**:
  - `nginx_logs`: External volume for Nginx logs.
  - `elasticsearch`: Persistent volume for Elasticsearch data.
- **Networks**:
  - `elk`: Bridge network connecting all services.

## Troubleshooting

- **Logs**: Check container logs for each service using `docker logs <container_name>`.
- **Elasticsearch**: If it fails to start, check the data directory permissions and configurations.
- **Network Issues**: Ensure services are correctly connected to the `elk` network.