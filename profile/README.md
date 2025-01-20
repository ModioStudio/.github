## Welcome to the team 🙌

### Working Docker Compose

```YAML
version: '3.8'

services:
  frontend:
    image: ghcr.io/modiolabs/auth-frontend:latest
    container_name: auth-frontend
    ports:
      - "80:80"
    depends_on:
      - backend
    environment:
      - NODE_ENV=production
    networks:
      - app-network
  backend:
    image: ghcr.io/modiolabs/auth-backend:latest
    container_name: auth-backend
    ports:
      - "8080:8080"
    networks:
      - app-network
    depends_on:
      - postgres
  postgres:
    image: 'postgres:latest'
    container_name: auth-postgres
    environment:
      - 'POSTGRES_DB=authdb'
      - 'POSTGRES_PASSWORD=secret'
      - 'POSTGRES_USER=authadmin'
    ports:
      - '5432'
    networks:
      - app-network

networks:
  app-network:
    driver: bridge
```
