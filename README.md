# DevOps Toolkit

Infraestructura centralizada para gestionar servicios DevOps con Docker Compose.

## Estructura

| Servicio        | Descripción                                      | Puerto(s)          |
|-----------------|--------------------------------------------------|---------------------|
| **Traefik**     | Reverse proxy y gestión de certificados TLS      | 80, 443, 8080      |
| **Observability** | Monitoreo con Prometheus, Grafana y Loki       | 3000, 9090         |
| **Portainer**   | Gestión visual de contenedores Docker            | 9443               |

## Requisitos

- Docker >= 24.0
- Docker Compose >= 2.20
- Un dominio apuntando al servidor (para TLS con Let's Encrypt)

## Inicio rápido

```bash
# 1. Configurar variables de entorno
cp shared/env.example shared/.env

# 2. Crear la red compartida
docker network create proxy

# 3. Levantar Traefik (reverse proxy)
cd traefik && docker compose up -d

# 4. Levantar observabilidad
cd ../observability && docker compose up -d

# 5. Levantar Portainer
cd ../portainer && docker compose up -d
```

## Red compartida

Todos los servicios se conectan a la red externa `proxy`. Esto permite que Traefik enrute tráfico hacia cualquier contenedor sin exponer puertos directamente.

## Variables de entorno

Copiar `shared/env.example` a `shared/.env` y ajustar los valores antes de levantar los servicios.

## Detener todo

```bash
for dir in traefik observability portainer; do
  (cd "$dir" && docker compose down)
done
```
