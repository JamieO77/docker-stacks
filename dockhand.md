# Dockhand Container Management

## Overview
Dockhand is a streamlined, web-based graphical user interface (GUI) designed for the administration of Docker environments. It abstracts the complexities of the Docker CLI, providing a centralized dashboard to deploy microservices, monitor container health, inspect logs, and manage storage volumes. It serves as the primary orchestration layer for deploying and maintaining the standardized `.yml` stacks within this repository.

---

## First Steps Guide

### 1. Accessing the Dashboard
* Navigate to your designated Dockhand IP address and port in a web browser (e.g., `http://localhost:<PORT>`).
* Authenticate using your administrative credentials.

### 2. Deploying a New Stack
Dockhand utilizes standard Docker Compose syntax for deployment.
* Navigate to the **Stacks** or **Compose** section in the left-hand navigation pane.
* Select **Add Stack** or **Create New**.
* Define a clear, lowercase identifier for the stack (e.g., `lanman_project` or `openclaw_agent`).
* Copy the raw contents of your `.yml` file and paste it into the integrated web editor.
* Click **Deploy**. Dockhand will automatically pull the required images from the registry, configure the defined networks, mount the volumes, and initialize the containers.

### 3. Container Lifecycle Management
Once a stack is active, navigate to the **Containers** view to manage individual services.
* **Logs:** Click the document icon next to a container to view real-time `stdout` and `stderr` outputs. This is critical for verifying initialization sequences (e.g., database schema creation).
* **Console/Terminal:** Click the `>_` terminal icon to drop directly into an interactive shell (`/bin/bash` or `/bin/sh`) inside the running container for manual script execution or debugging.
* **State Control:** Use the action buttons to gracefully Stop, Restart, or aggressively Kill a misbehaving container.

### 4. Volume & Network Administration
* **Volumes:** Navigate to the Volumes tab to inspect persistent storage. Here, you can identify orphaned data or manually remove volumes from decommissioned stacks (`docker volume rm`).
* **Networks:** View active bridge networks to ensure isolated stacks are successfully communicating or to identify overlapping subnet allocations.

---

## Troubleshooting

### 1. Stack Deployment Failures
* **Port Conflicts:** If Dockhand throws a `Bind for 0.0.0.0:<port> failed` error, another service on the host is already utilizing that port. Modify the left side of the port mapping in your `.yml` (e.g., change `"8080:80"` to `"8085:80"`).
* **YAML Parsing Errors:** Docker Compose is strictly indentation-dependent. Ensure you are using spaces (not tabs) and that array lists (like `environment:` or `ports:`) are properly aligned.

### 2. Container Stuck in "Restarting" Loop
* Immediately access the container's **Logs** in Dockhand.
* This behavior typically indicates a fatal crash upon startup, often caused by missing environment variables, incorrect database credentials, or a missing volume mount pathway.

### 3. "Cannot Connect to Docker Daemon"
* If Dockhand itself loses connection to your containers, the host's Docker socket permissions may have reset. Ensure the Dockhand container has read/write access to `/var/run/docker.sock` on the host machine.

---

## Administrative Tips

* **Tag Specificity:** Avoid deploying images with the `:latest` tag in production environments. Pin specific version numbers (e.g., `mysql:8.0.35`) to prevent unintended breaking changes during automated pulls.
* **Environment Variable Abstraction:** Utilize Dockhand's built-in `.env` variable fields when deploying stacks to keep sensitive passwords out of your raw YAML configurations.
* **Routine Maintenance:** Periodically navigate to the Images and Volumes sections to manually prune unused, dangling assets to reclaim host storage space.
