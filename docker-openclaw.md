# OpenClaw Autonomous AI Agent Architecture

## Purpose
A containerized deployment of OpenClaw, a self-hosted autonomous AI agent. This stack isolates the agent's execution environment while providing persistent storage for its memory, skills, and workspace files. It serves as a secure local gateway to connect large language models (such as Claude, OpenAI, or local vLLM instances) directly to messaging platforms (Telegram, WhatsApp, Discord) and local execution tasks.

## Service Components

### 1. Agent Gateway (`openclaw_gateway`)
* **Role:** Primary long-running daemon managing API connections, background cron jobs, and the web-based Control UI.
* **Configuration:**
  * Accessible via host port `18789`.
  * Timezone strictly defined as `Europe/Lisbon` to ensure accurate calendar management and scheduled job execution.
* **Storage:** * Mounts the `openclaw_config` volume to `/home/node/.openclaw` for persisting API keys, interaction history, and system settings.
  * Mounts the `openclaw_workspace` volume to `/home/node/openclaw/workspace` as the isolated sandbox where the agent can safely read, write, and manipulate files autonomously.

## Volume Topology
This stack utilizes two managed Docker volumes to strictly separate the agent's configuration secrets from its active working directory, maintaining a secure boundary between the autonomous agent and the host operating system.
