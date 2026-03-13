# Local Large Language Model (LLM) Architecture

## Purpose
A containerized, offline-capable infrastructure for hosting and interacting with Large Language Models. This stack provides a secure, private backend inference engine coupled with a comprehensive web-based graphical user interface. It ensures sensitive data and proprietary prompts remain strictly on the local hardware, eliminating reliance on external cloud APIs.

## Service Components

### 1. Inference Engine (`ollama`)
* **Role:** Backend execution environment for quantized LLMs (e.g., Llama 3, Mistral, Qwen). 
* **Configuration:**
  * Accessible via host port `11434` for REST API integration (compatible with n8n and OpenClaw).
  * Timezone strictly defined as `Europe/Lisbon`.
  * Prepared for hardware acceleration via the Docker `deploy` specification (requires NVIDIA drivers and toolkit on the host system).
* **Storage:** Mounts the `ollama_data` volume to persist downloaded model weights across container restarts, preventing redundant multi-gigabyte downloads.

### 2. Graphical User Interface (`open_webui`)
* **Role:** Frontend chat interface, prompt management system, and document parsing utility (RAG).
* **Configuration:**
  * Accessible via host port `3005`.
  * Integrates directly with the `ollama` container via the internal Docker network (`OLLAMA_BASE_URL=http://ollama:11434`).
  * Authentication disabled by default (`WEBUI_AUTH=False`) for rapid local access.
* **Storage:** Mounts the `open_webui_data` volume to persist chat histories, custom system prompts, and uploaded reference documents.

## Volume Topology
This architecture relies on two persistent Docker volumes to isolate massive model binaries (`ollama_data`) from user interaction history and frontend configurations (`open_webui_data`).
