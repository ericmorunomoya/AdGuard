# Práctica AdGuard Home - Filtrado DNS con Docker

Esta práctica consiste en el despliegue de AdGuard Home mediante Docker Compose para actuar como un servidor DNS con capacidades de filtrado y bloqueo de publicidad/rastreo.

## Arquitectura del Despliegue

- **Imagen**: `adguard/adguardhome`
- **Puerto Web**: 3000 (Administración)
- **Puerto DNS**: 53 (TCP/UDP)
- **Volúmenes**: 
  - `workdir`: Datos de trabajo de la aplicación.
  - `confdir`: Ficheros de configuración persistentes.

## Fichero Docker Compose

```yaml
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "3000:3000/tcp"
    volumes:
      - ./workdir:/opt/adguardhome/work
      - ./confdir:/opt/adguardhome/conf
    restart: unless-stopped
```

## Pasos Realizados

1. **Despliegue**: Se ha creado el fichero `docker-compose.yml` y se ha levantado el servicio con `docker-compose up -d`.
2. **Configuración Inicial**: Se ha accedido a `http://localhost:3000` para configurar el usuario administrador y las interfaces de red.
3. **Activación de Filtros**: Se han verificado las listas de bloqueo activas (AdGuard DNS filter).
4. **Comprobación de Bloqueo**: Se ha realizado una consulta DNS al dominio `doubleclick.net` apuntando al servidor local, verificando que devuelve `0.0.0.0` (bloqueado).

## Capturas de Pantalla

Las capturas se encuentran en la carpeta `/capturas`:
- `01_listas_bloqueo.png`: Listas de filtrado configuradas.
- **Panel de Control (Desglosado):**
  - `02a_dashboard_resumen.png`: Resumen de consultas y bloqueos.
  - `02b_dashboard_estadisticas.png`: Estadísticas generales de tráfico.
  - `02c_dashboard_clientes.png`: Clientes con más peticiones.
  - `02d_dashboard_dominios_consultados.png`: Dominios más solicitados.
- `03_registro_consultas_bloqueo.png`: Registro de consultas detallado con bloqueo verificado.

---
**Eric Moruno Moya**
Instituto El Calamot - 2026
