# Document & Media Processing Architecture

## Purpose
A containerized utility stack dedicated to heavy file manipulation and localized conversion. This infrastructure provides a comprehensive web-based suite for PDF editing and Optical Character Recognition (OCR), alongside an automated, hardware-accelerated video transcoding node that integrates directly with external Network-Attached Storage (NAS).

## Service Components

### 1. Document Processing Engine (`stirling-pdf`)
* **Image:** `stirlingtools/stirling-pdf:latest`
* **Role:** Centralized platform for PDF manipulation, conversion, and OCR capabilities.
* **Configuration:**
  * Accessible via host port `8081`.
  * Configured explicitly for local network access (`DOCKER_ENABLE_SECURITY=false`, `HOST=0.0.0.0`).
  * Timezone explicitly set to `Europe/Lisbon` to ensure accurate timestamping on processed documents.
* **Storage:** Utilizes `stirling_configs` for application state and `stirling_training_data` mounted to `/usr/share/tessdata` to retain Tesseract OCR language packs persistently.

### 2. Video Transcoding Node (`handbrake`)
* **Image:** `jlesage/handbrake:latest`
* **Role:** Automated and manual video encoding engine utilizing an embedded VNC web interface.
* **Configuration:**
  * Accessible via host port `5800` through a browser-based VNC client (`ENABLE_VNC=1`).
  * Maps the host's `/dev/dri` hardware device directly into the container, enabling hardware-accelerated video encoding (e.g., Intel QuickSync or AMD VCE).
  * Timezone aligned to `Europe/Lisbon`.
* **Storage:** * Retains application configuration in the `handbrake_config` Docker volume.
  * Implements a direct media pipeline connecting to a designated NAS (`//Tank-SOHO`). It reads source files securely in read-only mode (`/storage:ro`), monitors a drop-folder for automated queueing (`/watch:rw`), and writes finished encodes to an output directory (`/output:rw`).

## Volume Topology
This stack relies on a hybrid storage approach. It utilizes local Docker volumes (`stirling_training_data`, `stirling_configs`, `handbrake_config`) for application state, while directly interfacing with Windows/SMB UNC paths (`//Tank-SOHO`) to process large, externally hosted media files without duplicating data locally. *Note: A `filebrowser_config` volume is declared in the architecture but remains unallocated in the current service definitions.*
