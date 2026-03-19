# Personal Docker Stack Repository

### You will need to adust stacks with your own usernames, passwords, keys, and secrets where required!
## Overview
A centralized repository of containerized architectures utilized for web development, network diagnostics, document processing, and workflow automation. 

**Deployment Notice:** Prior to executing `docker compose up -d`, you must review and modify each `docker-compose.yml` file. Explicitly adjust environment variables, administrative credentials, mapped host ports, and persistent volume paths to align with your local host environment.

---

## Repository Index

### First Start - Docker installed....
See 1st start Docker and Dockhand for a small guide on how to setup docker with dockhand for web based management of your docker environment
* **How to Stack:** [View Guide ](./docker-start-guide.md)
* **Docker Web Management Stack:** [`dockhand.yml`](./dockhand.yml) | [View Documentation](./dockhand.md)

### Web Development
Containerized environments tailored for Scriptcase and PHP application deployment.
* **Core Development Stack:** [`docker-dev-stack.yml`](./docker-dev-stack.yml) | [View Architecture Documentation](./docker-dev-stack.md)

### Developer Tools & Diagnostics
Lightweight utility stacks for frontend UI/UX prototyping, API testing, and network OSINT reconnaissance.
* **Web Developer Utilities:** [`docker-dev-tools.yml`](./docker-dev-tools.yml) | [View Architecture Documentation](./docker-dev-tools.md)
* **LAN Monitoring & OSINT:** [`docker-lan-tools.yml`](./docker-lan-tools.yml) | [View Architecture Documentation](./docker-lan-tools.md)

### Office & Media Production
Hardware-accelerated and localized processing nodes for heavy file manipulation.
* **Document & Media Tools:** [`docker-pdf-tools-stack.yml`](./docker-pdf-tools-stack.yml) | [View Architecture Documentation](./docker-pdf-tools-stack.md)

### Automation Services
Horizontally scalable architectures for enterprise-grade webhook routing and background task execution.
* **n8n Workflow Engine:** [`docker-n8n-stack.yml`](./docker-n8n-stack.yml) | [View Architecture Documentation](./docker-n8n-stack.md)

### Artificial Intelligence (is it...) Agentic maybe
Self-hosted autonomous AI agent gateways and local execution environments.
* **OpenClaw Autonomous Agent:** [`docker-openclaww.yml`](./docker-openclaw.yml) | [View Architecture Documentation](./docker-openclaw.md)
* **Ollama Lareg Language Model or LLM:** [`docker-ollama.yml`](./docker-ollama.yml) | [View Architecture Documentation](./docker-ollama.md)
  
### Specialized Projects
Dedicated microservice infrastructures for specific custom applications.
* **Lanman Network Scanner:** [`lanman-dock/docker-compose.yml`](./lanman-dock/docker-compose.yml) | [View Architecture Documentation](./lanman-dock/README.md)
  
* **Lanman Network Scanner - HOST:** [`docker-lanman-host/docker-compose.yml`](./docker-lanman-host/docker-compose.yml) | [View Architecture Documentation](./lanman-dock/README.md)
* **Lanman Network Scanner - WORKER:** [`docker-lanman-worker/docker-compose.yml`](./docker-lanman-worker/docker-compose.yml) | [View Architecture Documentation](./lanman-dock/README.md)
