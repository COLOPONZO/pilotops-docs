# Notificaciones

## Objetivo

PilotOps utiliza notificaciones push para informar al práctico sobre cambios relevantes de su estado operativo.

Entre los eventos previstos se encuentran:

- cambios de estado;
- llegada a posición 1 en espera;
- transición a trabajo en proceso;
- otros eventos operativos que se incorporen en el futuro.

## Arquitectura

El flujo de notificaciones es:

PilotOps iOS → registro del dispositivo → Oracle → APNS → iPhone

El servidor Oracle mantiene los tokens de dispositivos registrados y envía las notificaciones mediante Apple Push Notification Service (APNS).

## Registro de dispositivos

PilotOps iOS registra el dispositivo mediante:

`http://163.176.64.85:55050/register_device`

El servicio correspondiente es:

`pilotops-push.service`

El registro incluye:

- nombre del práctico;
- device token APNS.

Los tokens se almacenan en la tabla:

`usuarios_push`

de:

`pilotops_guardias.db`

## APNS

Configuración utilizada:

- Team ID: `799QJ489HL`
- Key ID: `N89W38H5JN`
- Bundle ID: `Daniel-Ponzo.PilotOps`

Para las instalaciones distribuidas mediante TestFlight se utiliza el entorno APNS de producción:

`https://api.push.apple.com`

Las instalaciones directas desde Xcode utilizan el entorno sandbox:

`https://api.sandbox.push.apple.com`

Un token APNS pertenece al entorno en el que fue generado. Un token sandbox enviado al servidor de producción, o viceversa, puede producir:

`BadDeviceToken`

## TestFlight

La versión validada durante la migración al nuevo Oracle fue:

`PilotOps 1.2 (3)`

Después de instalar o actualizar PilotOps mediante TestFlight, la aplicación debe abrirse para permitir que el token actual del dispositivo sea registrado en el servidor.

## Prueba de producción

El 12 de agosto de 2026 se verificó el flujo completo:

1. PilotOps 1.2 (3) fue instalada mediante TestFlight.
2. La aplicación registró un nuevo device token en Oracle.
3. El token apareció en `usuarios_push`.
4. Oracle envió una notificación mediante APNS producción.
5. APNS respondió HTTP 200.
6. La notificación fue recibida correctamente en el iPhone.

Esto confirmó el funcionamiento completo:

PilotOps → Oracle → APNS → iPhone

## Herramientas de prueba

El archivo:

`send_push.py`

permite realizar pruebas manuales de APNS.

El proceso automático de notificaciones se encuentra integrado en:

`monitor_turno.py`

Para producción, `monitor_turno.py` debe utilizar:

`https://api.push.apple.com`

## Consideraciones

No debe asumirse que un token anterior continúa siendo válido después de:

- reinstalar la aplicación;
- cambiar de dispositivo;
- cambiar entre instalación Xcode y TestFlight;
- cambiar el entorno APNS.

El servidor debe utilizar siempre el token registrado por la instalación actual.

Los dispositivos de todos los testers deben abrir PilotOps después de actualizar a una versión que apunte al nuevo servidor para que sus tokens queden registrados correctamente.
