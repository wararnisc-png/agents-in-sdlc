---
title: "Lección 12 - Publica el sitio con GitHub Pages"
description: "Usa la aplicación GitHub Copilot para configurar un flujo de trabajo de Pages, revisar su solicitud de cambios y comprobar que Space Quiz está disponible."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Publica Space Quiz en Internet con GitHub Pages. Copilot puede preparar el flujo de trabajo y guiarte en el despliegue, pero tú eres responsable de revisar los cambios y confirmar que el sitio está disponible.

En esta lección:

- pedirás a Copilot que configure una implementación en GitHub Pages.
- revisarás el flujo de trabajo y la solicitud de cambios antes de combinarla.
- seguirás la implementación y comprobarás el sitio publicado.

## Situación

Space Quiz ya está en un repositorio de GitHub, pero la gente todavía necesita una forma sencilla de probarlo. Publicar el sitio de un solo archivo con GitHub Pages permite acceder a él mediante una URL pública, sin añadir un servidor ni dependencias de ejecución.

## Pide a Copilot que prepare la implementación

> [!WARNING]
> Crear una solicitud de cambios puede confirmar y enviar código. Revisa la configuración de aprobaciones y el repositorio de destino antes de enviar este mensaje. Si seleccionas **Approve all**, no esperes otro aviso de confirmación.

En la sesión de la aplicación Copilot para `space-quiz`, envía este mensaje:

```plaintext
Prepara el despliegue en GitHub Pages para este repositorio. Crea un flujo de trabajo de GitHub Actions que compile el sitio si hace falta y lo publique en GitHub Pages cuando los cambios lleguen a la rama predeterminada. Si todavía no hay un archivo README, añade uno que describa la aplicación y explique cómo ejecutarla en local. Crea una solicitud de cambios con estas modificaciones e indica su enlace y cualquier configuración o permiso necesario de Pages. No combines la solicitud, no habilites la combinación automática, no cambies la configuración de Pages ni publiques el sitio. Detente y espera a que revise los cambios.
```

## Revisa el flujo de trabajo y la solicitud de cambios

1. Confirma que el archivo README solo se añade si el repositorio todavía no tiene uno.
2. Revisa los cambios de la solicitud, incluidos los pasos de compilación y despliegue del flujo de trabajo, sus desencadenadores y permisos.
3. Confirma que el flujo de trabajo implementa desde la rama predeterminada, no desde una solicitud de cambios que aún no se haya combinado.
4. Solicita las correcciones necesarias y revisa el diff actualizado. Espera a que se superen las comprobaciones obligatorias de la solicitud antes de autorizar la combinación.

## Autoriza la combinación y el despliegue

> [!WARNING]
> El siguiente mensaje autoriza al agente a combinar la solicitud de cambios revisada, modificar la configuración de Pages del repositorio y publicar el sitio. Envíalo solo después de terminar la revisión y confirmar el repositorio y la solicitud. La configuración de aprobaciones podría permitir estas acciones sin pedir otra confirmación.

Sustituye `<PR_NUMBER>` por el número de la solicitud de cambios que has revisado y envía este mensaje por separado:

```plaintext
He revisado la solicitud de cambios <PR_NUMBER> de este repositorio y autorizo su combinación e implementación. Habilita GitHub Pages mediante GitHub Actions, combina esa solicitud solo cuando se superen las comprobaciones obligatorias y supervisa la implementación hasta que finalice correctamente. Indica la URL final del sitio publicado. Si no tienes permiso para habilitar Pages o combinar la solicitud, explícame exactamente qué debo aprobar o hacer; no indiques que ha terminado correctamente hasta que el sitio esté publicado.
```

![Diagrama de tres fases: una solicitud de cambios de space-quiz combinada; una ejecución correcta de Deploy website en GitHub Actions con los pasos Build website, Upload artifact y Deploy to Pages; y Space Quiz publicado en yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Comprueba la implementación

1. Sigue la ejecución de implementación de GitHub Actions hasta que finalice correctamente.
2. Abre la URL indicada y confirma que se carga Space Quiz.

Si el agente no puede habilitar Pages o combinar la solicitud, sigue las instrucciones concretas que te proporcione. No des la tarea por terminada hasta que la implementación finalice correctamente y el sitio esté disponible.

## Resumen y siguientes pasos

Space Quiz ya está disponible y has comprobado la implementación en lugar de confiar únicamente en el informe del agente. Continúa con la [Lección 13: Revisión y siguientes pasos][next-lesson].

[next-lesson]: ../13-review/
