version: '3.8'

services:
  # 1. MySpeed: Automated Speedtests
  myspeed:
    image: germannewsmaker/myspeed:latest
    container_name: myspeed
    ports:
      - "5216:5216"
    volumes:
      - myspeed_data:/myspeed/data
    environment:
      - BIND=0.0.0.0
    restart: unless-stopped

  # 2. Web-Check: Website OSINT
  web-check:
    image: lissy93/web-check:latest
    container_name: web-check
    ports:
      - "3001:3000"
    environment:
      - HOST=0.0.0.0
      - TRUST_PROXY=true
    restart: unless-stopped

  # 3. Portracker: Monitor Docker/Host Ports
  portracker:
    image: mostafawahied/portracker:latest
    container_name: portracker
    ports:
      - "4999:4999"             # Standard port mapping for Windows
    environment:
      - SESSION_SECRET=ADD_YOUR_OWN_SECRET_KEY
      - AUTH_ENABLED=true        # Enable authentication
      - AUTH_USERNAME=admin      # Set your username
      - AUTH_PASSWORD=ADD_YOUR_OWN_PASSWORD  # Set your password
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - portracker_data:/data
    restart: unless-stopped

volumes:
  myspeed_data:
  portracker_data:
