# docunube/stacks


Git repo para desplegar **Paperless‑ngx**, **Stirling‑PDF** y **Vaultwarden** en un NAS Synology (DSM 7.2.2) mediante **Portainer** usando *Deploy from Git*.


## Estructura
```
/README.md
/.gitignore
/paperless/
├─ docker-compose.yml
└─ .env.example
/stirling-pdf/
├─ docker-compose.yml
└─ .env.example
/vaultwarden/
├─ docker-compose.yml
└─ .env.example
```


## Flujo (Git → Portainer)
1) Edita los *.env.example* y **NO** subas secretos.
2) Crea el *Stack* en Portainer con "Git repository" apuntando a este repo y la ruta del compose correspondiente.
3) En la pestaña **Environment variables** introduce los valores reales de las variables.
4) Publicamos cambios en Git para versionar modificaciones.


## DNS y Reverse Proxy
- Todos los servicios escuchan sólo en `127.0.0.1` con puertos internos.
- DSM Reverse Proxy:
- `gesdoc.docunube.com` → `http://127.0.0.1:${PAPERLESS_HTTP_PORT}`
- `pdf.docunube.com` → `http://127.0.0.1:${STIRLING_HTTP_PORT}`
- `boveda.docunube.com` → `http://127.0.0.1:${VAULTWARDEN_HTTP_PORT}`
- Certificados: Let’s Encrypt desde DSM y asignar a cada host.


## Backups
- Copias diarias de `/volume1/docker/<servicio>/...` y configuración de Portainer.