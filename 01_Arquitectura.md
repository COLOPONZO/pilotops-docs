# Arquitectura

## Propósito

Este documento define la arquitectura general vigente de PilotOps Platform.

Su objetivo es establecer cómo se organizan los componentes principales, cuál es la fuente de información operativa y qué responsabilidades tiene cada parte del sistema.

## Visión general

PilotOps Platform está formada por aplicaciones móviles nativas, servicios backend y documentación técnica.

La plataforma se basa en una idea central: las aplicaciones móviles obtienen la información operativa directamente desde Operaciones Portuarias, mientras que el backend se reserva para servicios comunes como notificaciones, logs, analytics y monitoreo.

## Componentes principales

### PilotOps iOS

Aplicación nativa para iPhone.

Su responsabilidad es autenticar al usuario, mantener la sesión, obtener información operativa desde Operaciones Portuarias y presentarla en una interfaz móvil.

También recibe notificaciones push mediante APNS.

### PilotOps Android

Aplicación nativa para Android.

Debe ofrecer funcionalidad equivalente a PilotOps iOS, respetando las características propias de Android.

Su responsabilidad es autenticar al usuario, mantener la sesión, obtener información operativa desde Operaciones Portuarias y presentarla en una interfaz móvil.

También recibirá notificaciones push mediante Firebase Cloud Messaging.

### PilotOps Backend

Backend de servicios comunes.

Su responsabilidad no es reemplazar a Operaciones Portuarias como fuente de datos, sino brindar servicios transversales a la plataforma.

Entre sus funciones se incluyen:

- registro de dispositivos;
- envío de notificaciones;
- logs;
- analytics;
- monitoreo;
- procesos programados.

### PilotOps Docs

Repositorio oficial de documentación técnica.

Su función es registrar la arquitectura, los estándares, el modelo de datos, las integraciones, las decisiones técnicas y la evolución del proyecto.

## Fuente de información operativa

La fuente oficial de información operativa es Operaciones Portuarias.

Las aplicaciones móviles acceden a esa información mediante:

- autenticación web;
- cookies de sesión;
- lectura de HTML;
- parsing;
- scraping.

El backend no replica esos datos como fuente principal.

## Arquitectura de alto nivel

```text
Operaciones Portuarias
        │
        │ Login web + cookies
        │ HTML
        ▼
Scraping en clientes móviles
        │
        ├── PilotOps iOS
        │
        └── PilotOps Android
                │
                ▼
        PilotOps Backend
        Push · Logs · Analytics · Monitoreo