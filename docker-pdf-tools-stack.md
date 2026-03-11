version: '3.8'

services:
  # 1. Stirling-PDF: (Port 8081)
  stirling-pdf:
    image: stirlingtools/stirling-pdf:latest
    container_name: stirling-pdf
    ports:
      - "8081:8080"
    environment:
      - TZ=Europe/Lisbon
      - DOCKER_ENABLE_SECURITY=false
      - HOST=0.0.0.0
    volumes:
      - stirling_training_data:/usr/share/tessdata
      - stirling_configs:/configs
    restart: unless-stopped

  # 2. Handbrake: (Port 5800)
  handbrake:
    image: jlesage/handbrake:latest
    container_name: handbrake
    ports:
      - "5800:5800"
    devices:
      - /dev/dri:/dev/dri 
    volumes:
      - handbrake_config:/config:rw
      # FIXED WINDOWS PATHS BELOW:
      - "//Tank-SOHO/Media/media_convert/videos:/storage:ro"
      - "//Tank-SOHO/Media/media_convert/convert:/watch:rw"
      - "//Tank-SOHO/Media/media_convert/output:/output:rw"
    environment:
      - TZ=Europe/Lisbon
      - KEEP_APP_RUNNING=1
      - ENABLE_VNC=1
      - HOST=0.0.0.0
    restart: unless-stopped

volumes:
  stirling_training_data:
  stirling_configs:
  handbrake_config:
  filebrowser_config:
