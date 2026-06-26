# Estándares

## Propósito

Este documento define las reglas de desarrollo de PilotOps Platform.

Su objetivo es mantener una arquitectura consistente, un estilo de trabajo uniforme y una base de código fácil de mantener en todas las plataformas que integran el proyecto.

---

## Principios generales

Todo desarrollo realizado dentro de PilotOps Platform deberá respetar los siguientes principios:

- simplicidad;
- claridad;
- modularidad;
- consistencia;
- documentación actualizada;
- responsabilidad única.

Cuando exista conflicto entre rapidez y calidad de diseño, deberá priorizarse la calidad del diseño.

---

## Organización de proyectos

Cada componente principal de la plataforma mantiene su propio repositorio Git.

Actualmente la plataforma se organiza en:

- pilotops-ios
- pilotops-android
- pilotops-backend
- pilotops-docs

El directorio `pilotops-platform` funciona únicamente como workspace y no posee repositorio Git propio.

---

## Flujo de trabajo

Toda funcionalidad deberá seguir el siguiente proceso:

1. Análisis.
2. Diseño.
3. Documentación.
4. Implementación.
5. Pruebas.
6. Commit.

No deberán implementarse cambios importantes sin definir previamente su ubicación dentro de la arquitectura.

---

## Documentación

La documentación forma parte del producto.

Toda decisión técnica relevante deberá quedar documentada.

La documentación se redactará en formato Markdown.

Cada documento deberá tener un único propósito claramente definido.

No deberá duplicarse información existente en otros documentos.

---

## Archivos

Cuando se modifique un archivo, se trabajará preferentemente con el archivo completo.

Esta regla aplica a:

- Swift
- Kotlin
- Python
- Markdown
- SQL
- Archivos de configuración

Los cambios parciales solo se utilizarán cuando sea necesario explicar una modificación puntual.

---

## Convenciones de nombres

Los repositorios utilizarán nombres en minúsculas separados por guiones.

Ejemplos:

- pilotops-ios
- pilotops-android
- pilotops-backend
- pilotops-docs

Las clases deberán utilizar nombres descriptivos y mantener la misma responsabilidad en todas las plataformas.

Ejemplos:

- LoginService
- SessionStore
- NetworkSession
- CambioEstadoService
- TrabajoProcesoService

Siempre que exista una funcionalidad equivalente entre iOS y Android, se procurará utilizar la misma nomenclatura.

---

## Separación de responsabilidades

La interfaz gráfica no deberá contener lógica de negocio.

Las operaciones de red, autenticación, scraping y acceso a datos deberán implementarse mediante servicios especializados.

Cada clase deberá tener una única responsabilidad claramente definida.

---

## Backend

El backend será responsable únicamente de los servicios comunes de la plataforma.

Entre ellos:

- registro de dispositivos;
- envío de notificaciones;
- analytics;
- logs;
- monitoreo;
- procesos programados.

No deberá reemplazar la fuente principal de información operativa salvo decisión arquitectónica documentada.

---

## Git

Cada proyecto mantiene un historial independiente.

Los commits deberán representar una única intención.

Ejemplos:

- Add architecture document v1.0
- Create Android login service
- Fix session validation
- Update push notification flow

Se recomienda realizar commits pequeños y frecuentes.

---

## Calidad

Antes de realizar un commit deberá verificarse:

- que el proyecto compile;
- que la funcionalidad haya sido probada;
- que la documentación se encuentre actualizada cuando corresponda.

---

## Evolución

Estos estándares podrán ampliarse con nuevas reglas siempre que no contradigan los principios definidos en este documento.

---

## Historial

| Versión | Fecha | Descripción |
|----------|--------|-------------|
| 1.0 | Junio 2026 | Creación inicial del documento. |