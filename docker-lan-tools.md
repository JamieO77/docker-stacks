# Network Diagnostics & OSINT Monitoring Architecture

## Purpose
A containerized infrastructure designed for continuous network performance tracking, external web asset reconnaissance, and internal Docker port management. This stack provides a unified local toolkit for diagnosing connectivity metrics, profiling external web servers, and auditing active port allocations across the Docker daemon.

## Service Components

### 1. Performance Diagnostics (`myspeed`)
* **Role:** Automated bandwidth and latency monitoring utility.
* **Configuration:**
  * Accessible via host port `5216`.
  * Executes scheduled Cron-based speed tests and generates historical performance graphs.
  * Binds to all interfaces (`BIND=0.0.0.0`).
* **Storage:** Utilizes the `myspeed_data` persistent volume to retain historical test results across container restarts.

### 2. External Reconnaissance (`web-check`)
* **Role:** Comprehensive Open-Source Intelligence (OSINT) and website analysis tool.
* **Configuration:**
  * Accessible via host port `3001` (routing to internal port `3000`).
  * Configured to trust reverse proxies (`TRUST_PROXY=true`) and bind to all host interfaces.
  * Aggregates DNS records, SSL certificate data, server headers, and routing architecture for targeted domains.

### 3. Internal Port Management (`portracker`)
* **Role:** Real-time visual dashboard for Docker and host port mapping.
* **Configuration:**
  * Accessible via host port `4999`.
  * Secures the dashboard utilizing built-in environment variable authentication (`AUTH_ENABLED`, `AUTH_USERNAME`, `AUTH_PASSWORD`).
  * Mounts the host's Docker socket (`/var/run/docker.sock`) in read-only mode (`ro`) to securely query the Docker daemon for active container port bindings.
* **Storage:** Utilizes the `portracker_data` volume for application state retention.

## Volume Topology
This stack utilizes two managed Docker volumes (`myspeed_data`, `portracker_data`) to ensure diagnostic history and application configurations are isolated from the container lifecycle.
