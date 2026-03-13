# LanMan Dock stack:
# Lanman Network Scanner & Web Platform Architecture
*Purpose
  A microservices architecture utilizing Docker to isolate the discrete components of the Lanman network discovery platform. This design ensures environment consistency, dependency isolation, and the secure execution of raw network scanning tasks alongside standard web delivery services.

#Service Components
* mysql (Database Node): A MySQL 8.0 container providing persistent relational data storage for network discovery logs, IP mapping, and platform configuration.
* phpmyadmin (Database Management): A web-based administration interface connected via the internal Docker bridge network to the MySQL container, allowing direct query execution and schema management.
* apache_php (Application Server): A custom-built PHP 8.2 and Apache container (Dockerfile.web). It is explicitly configured with the required PHP extensions (gd, pdo_mysql, mysqli, zip) and timezone settings to host the Scriptcase-generated Lanman frontend application.
* filebrowser (File Management): A lightweight, web-based file management interface volume-mapped directly to the Apache web root and the Python scripts directory. This enables direct file deployments and modifications without requiring SSH access to the host.
* python_scanner (Discovery Engine): A custom Python 3.11 environment (Dockerfile.scanner) running in host network mode with elevated Linux capabilities (NET_ADMIN, NET_RAW). It utilizes internal cron jobs to execute Scapy and Nmap scripts (scan.py, cleanup.py) for raw ARP/ICMP sweeps directly on the physical LAN, bypassing Docker's network isolation.
* linux_desktop (Administrative Node): A containerized Ubuntu XFCE desktop environment accessible via a web browser (port 3000). It provides an interactive terminal and GUI for ad-hoc network troubleshooting, manual script execution, and administrative tasks within the stack's bridged network space.
