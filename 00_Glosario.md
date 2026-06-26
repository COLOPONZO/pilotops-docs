# Glosario

## Propósito

Este documento define los términos principales utilizados en PilotOps Platform.

Su objetivo es mantener un lenguaje común entre la documentación, el código y las decisiones técnicas.

## Términos

### PilotOps Platform

Conjunto de proyectos que forman el ecosistema PilotOps: aplicaciones móviles, backend y documentación técnica.

### Workspace

Directorio local que agrupa los proyectos de la plataforma.

El workspace no es un repositorio Git.

### Repositorio

Proyecto independiente versionado con Git.

Cada componente principal de PilotOps tiene su propio repositorio.

### Cliente móvil

Aplicación utilizada por el usuario final.

En PilotOps existen dos clientes móviles:

- PilotOps iOS.
- PilotOps Android.

### Backend

Conjunto de servicios comunes utilizados por la plataforma.

En la arquitectura actual, el backend se utiliza para notificaciones, logs, analytics, monitoreo y procesos programados.

### Operaciones Portuarias

Sistema web externo desde donde se obtiene la información operativa principal.

### Scraping

Proceso mediante el cual las aplicaciones móviles obtienen información desde páginas HTML de Operaciones Portuarias.

### Sesión

Estado autenticado del usuario luego de iniciar sesión correctamente en Operaciones Portuarias.

### Cookie

Dato utilizado por el servidor web para mantener la sesión autenticada del usuario.

### Servicio

Componente responsable de ejecutar una operación concreta, como login, lectura de estado o lectura de trabajos.

### Store

Componente encargado de mantener estado compartido dentro de la aplicación.

### ViewModel

Componente que conecta la lógica de negocio con la interfaz visual.

### Push Notification

Notificación enviada al dispositivo del usuario desde el backend.

### APNS

Servicio de notificaciones push de Apple utilizado por iOS.

### FCM

Firebase Cloud Messaging. Servicio de notificaciones push utilizado por Android.

## Historial

| Versión | Fecha | Descripción |
|---|---|---|
| 1.0 | Junio 2026 | Creación inicial del glosario. |