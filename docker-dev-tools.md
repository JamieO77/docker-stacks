version: '3.8'

services:
  # 1. API TESTING (Postman Alternative)
  # Access at http://[YOUR-IP]:3000
  hoppscotch:
    image: hoppscotch/hoppscotch:latest
    container_name: hoppscotch
    restart: always
    ports:
      - "3004:3000"

  # 2. CORS PROXY (To make API testing work smoothly)
  # Access at http://[YOUR-IP]:9159
  hoppscotch-proxy:
    image: hoppscotch/proxyscotch:latest
    container_name: hoppscotch-proxy
    restart: always
    ports:
      - "9159:9159"

  # 3. THE DEV SWISS ARMY KNIFE (Colors & Tailwind Tools)
  # Access at http://[YOUR-IP]:8080
  it-tools:
    image: corentinth/it-tools:latest
    container_name: it-tools
    restart: always
    ports:
      - "8082:80"
    environment:
      - HOST=0.0.0.0

  # 4. PALETTE CREATOR (Visual Color Generator - No Login)
  # Access at http://[YOUR-IP]:5005
  palette-generator:
    image: noxone/shades:latest
    container_name: color-palette
    restart: always
    ports:
      - "5005:80"
    environment:
      - HOST=0.0.0.0

  # 5. TAILWIND PLAYGROUND (Simple & Instant)
  # Access at http://[YOUR-IP]:3001
  tailwind-tester:
    image: nginx:alpine
    container_name: tailwind-sandbox
    restart: always
    ports:
      - "3002:80"
