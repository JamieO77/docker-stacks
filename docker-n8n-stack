version: '3.8'
services:
  postgres:
    image: postgres:16
    restart: always
    environment:
      POSTGRES_USER: n8nuser_db
      POSTGRES_PASSWORD: ADD_YOUR_PASWORD
      POSTGRES_DB: n8n
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U n8nuser_db -d n8n"]
      interval: 5s
      timeout: 5s
      retries: 10
    labels:
      - "wud.registry=dockerhub"
      - "wud.trigger.auto=true"
    networks:
      - n8n_net

  redis:
    image: redis:7
    restart: always
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 5s
      timeout: 5s
      retries: 10
    labels:
      - "wud.registry=dockerhub"
      - "wud.trigger.auto=true"
    networks:
      - n8n_net

  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    restart: always
    environment:
      DB_TYPE: postgresdb
      DB_POSTGRESDB_HOST: postgres
      DB_POSTGRESDB_PORT: 5432
      DB_POSTGRESDB_DATABASE: n8n
      DB_POSTGRESDB_USER: n8nuser_db
      DB_POSTGRESDB_PASSWORD: ADD_YOUR_PASWORD
      QUEUE_MODE: true
      QUEUE_REDIS_URL: redis://redis:6379
      N8N_BASIC_AUTH_ACTIVE: true
      N8N_BASIC_AUTH_USER: ADD_YOUR_USERNAME
      N8N_BASIC_AUTH_PASSWORD: ADD_YOUR_PASWORD
      N8N_ENCRYPTION_KEY: ADD_YOUR_ENCRYPTION_KEY
      N8N_HOST: n8n.yourdomain.com
      N8N_PORT: 5678
      N8N_PROTOCOL: http
      NODE_ENV: production
      N8N_EDITOR_BASE_URL: https://n8n.yourdomain.com
      WEBHOOK_URL: https://n8n.yourdomain.com/
      N8N_ALLOWED_ORIGINS: https://n8n.yourdomain.com
      N8N_TRUST_PROXY: true
      N8N_PROXY_HOPS: 1
      N8N_DIAGNOSTICS_ENABLED: false
      N8N_RUNNERS_ENABLED: true
      N8N_RUNNERS_MODE: external
      N8N_RUNNERS_AUTH_TOKEN: ADD_YOUR_ENCRYPTION_KEY
      N8N_RUNNERS_BROKER_LISTEN_ADDRESS: 0.0.0.0
      N8N_PUSH_BACKEND: websocket
    ports:
      - "5678:5678"
    volumes:
      - n8n_data:/home/node/.n8n
    labels:
      - "wud.registry=ghcr"
      - "wud.trigger.auto=true"
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
      runners:
        condition: service_started
    networks:
      - n8n_net

  n8n-worker:
    image: docker.n8n.io/n8nio/n8n:latest
    restart: always
    command: worker
    environment:
      DB_TYPE: postgresdb
      DB_POSTGRESDB_HOST: postgres
      DB_POSTGRESDB_PORT: 5432
      DB_POSTGRESDB_DATABASE: n8n
      DB_POSTGRESDB_USER: ADD_YOUR_USERNAME
      DB_POSTGRESDB_PASSWORD: ADD_YOUR_PASWORD
      QUEUE_REDIS_URL: redis://redis:6379
      N8N_ENCRYPTION_KEY: ADD_YOUR_ENCRYPTION_KEY
      WEBHOOK_URL: https://n8n.yourdomain.com/
      NODE_ENV: production
      N8N_DIAGNOSTICS_ENABLED: false
      N8N_TRUST_PROXY: true
      N8N_PROXY_HOPS: 1
    volumes:
      - n8n_data:/home/node/.n8n
    labels:
      - "wud.registry=ghcr"
      - "wud.trigger.auto=true"
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_healthy
    networks:
      - n8n_net

  runners:
    image: n8nio/runners:latest
    restart: always
    environment:
      N8N_RUNNERS_AUTH_TOKEN: UBba5Sf(Rf)B1jN!4iN7%N3pvRQ7pk(5oz"7ZLs7DT(0rtJ&9rHX%pOR#6Fuc!TY
    labels:
      - "wud.registry=ghcr"
      - "wud.trigger.auto=true"
    networks:
      - n8n_net

volumes:
  postgres_data:
  n8n_data:

networks:
  n8n_net:
