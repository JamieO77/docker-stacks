# n8n Enterprise Workflow Automation Architecture

## Purpose
A highly scalable, production-ready containerized deployment for n8n. This architecture moves beyond the standard SQLite deployment by utilizing a robust PostgreSQL database and Redis-backed message queuing to enable horizontal scaling. It separates the core application (webhook/UI) from backend execution (workers/runners), ensuring complex automation workflows do not bottleneck the main user interface. 

## Service Components

### 1. Persistent Storage Layer (`postgres`)
* **Role:** Primary relational database for workflow definitions, execution history, and user credentials.
* **Configuration:**
  * Defines discrete user credentials (`n8nuser_db`).
  * Implements a rigorous health check using `pg_isready` to ensure database readiness before dependent services initialize.
  * Includes `wud` (What's Up Docker) labels for automated image update tracking.
* **Storage:** Utilizes the `postgres_data` volume for data persistence.

### 2. Message Broker Layer (`redis`)
* **Role:** In-memory data store managing the task queue for distributed execution.
* **Configuration:**
  * Implements a standard `redis-cli ping` health check.
  * Handles the delegation of workflow execution jobs from the main `n8n` instance to the `n8n-worker` instances.

### 3. Main Application Node (`n8n`)
* **Role:** Primary frontend interface, workflow editor, and webhook listener.
* **Configuration:**
  * Configured in `QUEUE_MODE: true`, delegating heavy processing to workers.
  * Secured via `N8N_BASIC_AUTH` and expects reverse proxy routing (`N8N_TRUST_PROXY`, `N8N_HOST`, `WEBHOOK_URL`).
  * Configured to interact with external Python/Node runners (`N8N_RUNNERS_MODE: external`).
  * Exposes port `5678` to the host for reverse proxy integration.
* **Dependencies:** Strictly requires `postgres` and `redis` to pass health checks before starting.
* **Storage:** Mounts the `n8n_data` volume for shared configuration files and SSH keys.

### 4. Background Execution Node (`n8n-worker`)
* **Role:** Dedicated execution engine for running workflows.
* **Configuration:**
  * Overrides the default command with `worker` to listen to the Redis queue rather than serving the UI.
  * Connects directly to the PostgreSQL database and Redis queue.
  * Can be horizontally scaled (e.g., `docker compose up --scale n8n-worker=3`) to handle higher execution loads.
* **Storage:** Mounts the same `n8n_data` volume as the main node to ensure access to required shared files.

### 5. Code Execution Environment (`runners`)
* **Role:** Isolated execution environment specifically for running Python and Node.js code blocks within n8n workflows.
* **Configuration:**
  * Authenticates with the main n8n application using a shared `N8N_RUNNERS_AUTH_TOKEN`.
  * Isolates custom code execution to prevent resource starvation or security breaches on the main n8n nodes.

## Network Topology
All services communicate securely over the internal `n8n_net` bridge network, exposing only the main n8n application port (`5678`) to the host environment for ingress routing.
