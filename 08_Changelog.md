# Changelog

## 2026-08-12 — Migración de producción a nuevo Oracle

### Backend

- Migración de los servicios de PilotOps al nuevo servidor Oracle.
- Nuevo servidor de producción: `163.176.64.85`.
- Verificación de acceso SSH.
- Habilitación y persistencia mediante `iptables-persistent` de los puertos:
  - `55050/tcp` — PilotOps Push Server.
  - `55051/tcp` — PilotOps Analytics API.
- Verificación externa de:
  - PilotOps Push Server.
  - PilotOps Analytics API.
- Puesta en funcionamiento de:
  - `pilotops-monitor.service`
  - `pilotops-push.service`
  - `pilotops-analytics.service`
  - `pilotops-finalizados.timer`

### PilotOps iOS

- Actualización de `PushRegistrationService.swift` para utilizar:
  - `http://163.176.64.85:55050/register_device`
- Compilación correcta de PilotOps.
- Corrección de duplicación de `@main` provocada por `PilotEntry.swift`.
- Distribución y prueba mediante TestFlight.
- Versión validada: `1.2 (3)`.
- Registro correcto del nuevo device token en Oracle.
- Repositorio `pilotops-ios` actualizado.
- Commit:
  - `2cb78ee Update push server to new Oracle instance`

### Notificaciones APNS

- Validación del entorno APNS de producción para instalaciones TestFlight.
- Confirmación de que tokens generados mediante instalación directa de Xcode utilizan sandbox.
- Prueba APNS de producción desde Oracle con respuesta HTTP 200.
- Recepción efectiva de la notificación en iPhone.
- Confirmación del flujo:
  - PilotOps → Oracle → APNS → iPhone.

### PilotOps Analytics iOS

- Actualización de la API al nuevo servidor:
  - `http://163.176.64.85:55051`
- Verificación de funcionamiento contra el nuevo Oracle.

### PilotOps Analytics Mac

- Se confirmó que la aplicación web local funciona en:
  - `http://127.0.0.1:5000`
- Se modificó `sync_all.sh` para dejar de sincronizar las bases desde Raspberry.
- Nueva sincronización mediante SCP directamente desde Oracle.
- Bases sincronizadas:
  - `pilotops_guardias.db`
  - `pilotops_operaciones.db`
- Verificación funcional de PilotOps Analytics Mac utilizando los datos del nuevo Oracle.

### Raspberry Pi

La Raspberry dejó de funcionar como servidor de producción.

Se detuvieron y deshabilitaron:

- `pilotops-monitor.service`
- `pilotops-push.service`
- `pilotops-analytics.service`
- `pilotops-finalizados.timer`

No se eliminaron archivos ni bases de datos.

La Raspberry queda conservada como respaldo y posible mecanismo de recuperación.

### Estado final

Al finalizar la migración se verificó el funcionamiento de:

- PilotOps iOS;
- registro de dispositivos push;
- APNS de producción;
- PilotOps Analytics iOS;
- PilotOps Analytics Mac;
- sincronización de bases desde Oracle;
- servicios backend del nuevo Oracle.

La Raspberry quedó fuera de producción para evitar procesos y notificaciones duplicadas.
