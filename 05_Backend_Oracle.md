# Backend Oracle

## Función

El servidor Oracle constituye el backend operativo compartido de PilotOps Platform.

La fuente principal de datos operativos continúa siendo Operaciones Portuarias mediante scraping directo desde las aplicaciones y procesos correspondientes.

Oracle se utiliza principalmente para:

- monitoreo de estados;
- notificaciones push;
- registro de dispositivos;
- almacenamiento de guardias y operaciones;
- sincronización de trabajos finalizados;
- API de PilotOps Analytics;
- servicios compartidos de la plataforma.

## Servidor activo

Servidor de producción:

- Usuario: `ubuntu`
- IP: `163.176.64.85`
- Directorio: `/home/ubuntu/pilotops-monitor`

## Bases de datos

Las bases SQLite principales son:

- `pilotops_guardias.db`
- `pilotops_operaciones.db`

`pilotops_guardias.db` contiene, entre otros datos, estados de guardia y dispositivos registrados para notificaciones push.

`pilotops_operaciones.db` contiene información utilizada para el historial y Analytics de operaciones.

## Servicios

El backend utiliza servicios systemd para mantener los procesos activos.

Servicios principales:

- `pilotops-monitor.service`
- `pilotops-push.service`
- `pilotops-analytics.service`
- `pilotops-finalizados.timer`
- `pilotops-finalizados.service`

### Monitor

`pilotops-monitor.service` ejecuta el monitoreo de cambios de estado y genera los eventos necesarios para las notificaciones.

### Push

`pilotops-push.service` expone el servicio de registro de dispositivos en el puerto:

`55050`

Endpoint utilizado por PilotOps iOS:

`/register_device`

### Analytics

`pilotops-analytics.service` expone la API de PilotOps Analytics en el puerto:

`55051`

Endpoint de comprobación:

`/analytics/health`

### Trabajos finalizados

`pilotops-finalizados.timer` ejecuta periódicamente el proceso de sincronización de trabajos finalizados.

## Acceso de red

Los puertos de producción habilitados son:

- `22/tcp` — SSH
- `55050/tcp` — PilotOps Push Server
- `55051/tcp` — PilotOps Analytics API

Las reglas correspondientes están persistidas mediante `iptables-persistent`.

## PilotOps Analytics Mac

PilotOps Analytics para macOS funciona localmente en:

`http://127.0.0.1:5000`

La aplicación utiliza bases SQLite locales.

El script:

`~/Projects/Analytics/sync_all.sh`

sincroniza actualmente:

- `pilotops_guardias.db`
- `pilotops_operaciones.db`

desde el servidor Oracle de producción mediante SCP.

La autenticación SSH utiliza:

`~/Projects/Analytics/Claves Oracle/ssh-key-2026-08-11.key`

## Raspberry Pi

La Raspberry Pi dejó de ser el servidor de producción el 12 de agosto de 2026.

Los siguientes componentes quedaron detenidos y deshabilitados:

- `pilotops-monitor.service`
- `pilotops-push.service`
- `pilotops-analytics.service`
- `pilotops-finalizados.timer`

Los archivos y bases de datos no fueron eliminados.

La Raspberry se conserva como respaldo y no debe ejecutar simultáneamente los servicios de producción mientras Oracle esté activo.

## Estado actual

Migración al nuevo servidor Oracle verificada el 12 de agosto de 2026.

Se comprobó:

- acceso externo al Push Server;
- acceso externo a Analytics API;
- registro de dispositivos desde PilotOps;
- envío APNS desde Oracle;
- recepción efectiva de notificaciones en iPhone;
- funcionamiento de PilotOps Analytics iOS;
- funcionamiento de PilotOps Analytics Mac;
- sincronización de las bases de Analytics Mac directamente desde Oracle.
