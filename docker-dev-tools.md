# Web Developer Utility & API Testing Architecture

## Purpose
A lightweight, containerized suite of frontend and backend developer utilities. This stack is designed to facilitate local API endpoint testing, CORS policy mitigation, data formatting, and UI/UX design. By hosting these tools locally, it ensures data privacy, offline capability, and removes dependencies on external SaaS platforms during active development.

## Service Components

### 1. API Testing Ecosystem (`hoppscotch`)
* **Role:** REST, GraphQL, and WebSocket API client interface.
* **Configuration:**
  * Accessible via host port `3004`.
  * Provides a comprehensive GUI for request construction, header management, and payload execution, serving as a localized alternative to Postman.

### 2. CORS Mitigation Proxy (`hoppscotch-proxy`)
* **Role:** Middleware for Cross-Origin Resource Sharing (CORS) resolution.
* **Configuration:**
  * Accessible via host port `9159`.
  * Intercepts outbound requests from the Hoppscotch client to append required cross-origin headers, preventing browser-level security blocks when testing local or strict APIs.

### 3. Developer Tool Aggregator (`it-tools`)
* **Role:** Centralized repository of cryptography, formatting, and conversion utilities.
* **Configuration:**
  * Accessible via host port `8082`.
  * Binds to all host interfaces (`HOST=0.0.0.0`). Provides localized, instantaneous access to JSON formatters, JWT decoders, hash generators, and base64 encoders.

### 4. UI/UX Color Engine (`palette-generator`)
* **Role:** Visual design tool for generating frontend color schemes.
* **Configuration:**
  * Accessible via host port `5005`.
  * Binds to all host interfaces (`HOST=0.0.0.0`). Facilitates the rapid creation, adjustment, and export of standardized color palettes for CSS frameworks like Tailwind.

### 5. Prototyping Sandbox (`tailwind-tester`)
* **Role:** Static web server for rapid HTML and CSS component isolation.
* **Configuration:**
  * Accessible via host port `3002`.
  * Utilizes a highly optimized Alpine-based Nginx instance to serve static assets instantly, providing a clean slate for testing UI components.

## Network Topology
This stack currently relies on the default Docker bridge network for inter-container communication and host port binding.
