# Scriptcase Development Environment Stack

## Purpose
A containerized web development environment optimized for Scriptcase applications. This stack provisions a legacy-compatible database, a pre-configured PHP/Apache web server with required Scriptcase extensions, and web-based utilities for database and file management. 

## Service Architecture

### 1. Database Layer (`mysql`)
* **Role:** Primary relational database management system.
* **Configuration:** * Exposes port `3306` to the host for external IDE connections.
  * Allows root connections from any host (`MYSQL_ROOT_HOST: '%'`).
  * Mounts a local `init.sql` script (`/c/DockerConfigs/init.sql`) to automatically seed the database on initial deployment.
* **Storage:** Utilizes the `mysql_data_v2` persistent volume.

### 2. Database Administration (`phpmyadmin`)
* **Role:** Web-based GUI for MySQL administration.
* **Configuration:**
  * Accessible via port `8084`.
  * Communicates securely with the database layer via the internal `devnet` bridge network.

### 3. Application Server (`apache-php`)
* **Role:** Web application server executing Scriptcase PHP code.
* **Configuration:**
  * Accessible via port `8089`.
  * Timezone strictly defined as `Europe/Lisbon`.
  * Executes a runtime `bash` initialization sequence to compile and enable essential PHP extensions (`gd`, `pdo_mysql`, `zip`, `mbstring`) required by the Scriptcase framework before starting the Apache foreground process.
* **Storage:** Mounts the `www_data_v2` volume for persistent application source code and binds a local `./logs` directory for Apache error/access tracking.

### 4. File Management (`filebrowser`)
* **Role:** Web-based file explorer and editor.
* **Configuration:**
  * Accessible via port `8083`.
  * Mounts multiple critical directories (`www_data_v2`, `mysql_data_v2`, `./logs`) to allow direct browser-based code editing, log monitoring, and file uploads without SSH protocol usage.

## Network Topology
All services operate on a single isolated Docker bridge network named `devnet`, enabling internal DNS resolution between containers (e.g., `phpmyadmin` communicating directly with `mysql`).
