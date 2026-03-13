# Personal Docker Stack Repository

## Overview
A centralized repository of containerized architectures utilized for web development, network diagnostics, document processing, and workflow automation. 

**Deployment Notice:** Prior to executing `docker compose up -d`, you must review and modify each `docker-compose.yml` file. Explicitly adjust environment variables, administrative credentials, mapped host ports, and persistent volume paths to align with your local host environment.

---

## Repository Index

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

### Specialized Projects
Dedicated microservice infrastructures for specific custom applications.
* **Lanman Network Scanner:** [`docker-lanman-stack.yml`](./docker-lanman-stack.yml) | [View Architecture Documentation](./docker-lanman-stack.md)
