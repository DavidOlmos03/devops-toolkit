# Traefik - Reverse Proxy

Reverse proxy con generación automática de certificados TLS via Let's Encrypt.

## Funcionalidades

- Redirección HTTP -> HTTPS automática
- Descubrimiento de servicios via Docker labels
- Dashboard protegido con Basic Auth
- Configuración dinámica en `dynamic/`

## Exponer un servicio

Agregar estas labels al contenedor que se quiera exponer:

```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.mi-app.rule=Host(`mi-app.${DOMAIN}`)"
  - "traefik.http.routers.mi-app.entrypoints=websecure"
  - "traefik.http.services.mi-app.loadbalancer.server.port=8080"
networks:
  - proxy
```

## Configuración dinámica

Agregar archivos `.yml` en `dynamic/` para middlewares, rate limiting, headers de seguridad, etc. Traefik los detecta automáticamente.
