# n8n with Docker Compose

This project runs [n8n](https://n8n.io) using Docker Compose, based on the official guide for [Docker Compose setup](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/).

For more configurations, see the [n8n-hosting repository](https://github.com/n8n-io/n8n-hosting).

## Troubleshooting

### 1. `Permission denied` for `init-data.sh`

If you see this error:
`/docker-entrypoint-initdb.d/init-data.sh: /bin/bash: bad interpreter: Permission denied`

**Solution:** Make the script executable before running `docker-compose up`.

```bash
chmod +x ./init-data.sh
```

### 2. Secure Cookie Error

If your browser shows this error:
`Your n8n server is configured to use a secure cookie, however you are either visiting this via an insecure URL, or using Safari.`

**Solution:** For local development, you can disable secure cookies. In `compose.yaml`, add the `N8N_SECURE_COOKIE=false` environment variable to the `n8n` service.

```yaml
# compose.yaml

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    environment:
      - N8N_SECURE_COOKIE=false   # Disable secure cookie
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=postgres
      ...
```

---