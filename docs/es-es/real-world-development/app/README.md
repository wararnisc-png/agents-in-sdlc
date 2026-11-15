---
slug: es-es/real-world-development/app
title: "Aplicación GitHub Copilot"
description: "Practica el desarrollo dirigido por agentes en la aplicación GitHub Copilot con sesiones paralelas, automatización de PR y lienzos compartidos."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La [**aplicación GitHub Copilot**](https://docs.github.com/copilot/concepts/agents/github-copilot-app) es una aplicación de escritorio basada en Copilot CLI que reúne el desarrollo dirigido por agentes en un único espacio de trabajo específico. Añade sesiones de agente en paralelo, modos de sesión intercambiables, lienzos compartidos y gestión nativa de incidencias y solicitudes de cambios de GitHub, incluido **Agent Merge**, que guía una solicitud durante las actualizaciones de base, los comentarios de revisión, las correcciones de integración continua (CI) y la combinación.

El taller sigue un flujo de trabajo continuo de Tailspin Toys:

1. Prepara el proyecto, instala la aplicación, conecta el repositorio y explora el espacio de trabajo y la lista de tareas inicial.
2. Añade valoraciones con estrellas, revisa el resultado en el navegador y combina manualmente tu primera solicitud de cambios (PR).
3. Parte de la incidencia de filtros, define el enfoque en el modo **Plan**, impleméntalo en el modo **Autopilot** y revísalo en el modo **Interactive**.
4. Actualiza las instrucciones del repositorio y aplícalas al trabajo de filtros.
5. Personaliza la aptitud `quality-checks` existente y úsala para ejecutar las comprobaciones del proyecto.
6. Añade el servidor Model Context Protocol (MCP) de Playwright y utilízalo para explorar los filtros en un navegador.
7. Crea un agente personalizado de control de calidad (QA) para revisar los requisitos, la cobertura y las pruebas de verificación.
8. Revisa el cambio completo de los filtros y utiliza Agent Merge para combinar la segunda PR.
9. Comprueba qué lienzos están disponibles; después, utiliza Database Explorer para crear y probar un lienzo de clasificación asociado al repositorio. Si no están disponibles las funciones necesarias, registra el bloqueo y utiliza la alternativa de solo lectura o continúa con el repaso.

Para mantener el taller centrado, crearás dos PR: una para las valoraciones con estrellas y otra para los filtros, junto con las actualizaciones de instrucciones y de la aptitud, el perfil de QA y las pruebas. Inicia cada una desde `main` actualizada. El flujo de filtros y calidad comparte una sesión, un árbol de trabajo y una rama para que puedas aprovechar el trabajo realizado mientras exploras cada herramienta. El ejercicio final del lienzo permanece en su sesión para que puedas centrarte en crear y probar la superficie compartida, en vez de repetir el flujo de PR.

## Lecciones

| Lección | Tema | Descripción |
|--------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Instala Node.js y crea una copia del proyecto Tailspin Toys |
| [1. Instala la aplicación Copilot][ex1] | Configuración | Instala la aplicación, conecta el proyecto y familiarízate con el espacio de trabajo |
| [2. Añade valoraciones con estrellas: una mejora rápida][ex2] | Primer cambio | Muestra las valoraciones existentes y la alternativa para los juegos sin puntuación, y combina la PR 1 |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica la funcionalidad desde su incidencia, impleméntala con Autopilot y revísala en Interactive |
| [4. Guía a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones y aplícalas a los filtros |
| [5. Personaliza y utiliza la aptitud quality-checks][ex5] | Comprobaciones repetibles | Explora la aptitud existente, cambia el formato del informe y ejecútala |
| [6. Valida la funcionalidad con Playwright MCP][ex6] | Observación en el navegador | Configura MCP desde Customize y examina el comportamiento de los filtros |
| [7. Crea y utiliza un agente de QA][ex7] | Requisitos y cobertura | Crea y selecciona un perfil especializado y reúne las pruebas de verificación finales |
| [8. Crea y combina la PR de la funcionalidad][ex8] | Revisión y combinación | Revisa los filtros, las instrucciones, la aptitud, el perfil de QA y las pruebas; después utiliza Agent Merge para combinar la segunda PR |
| [9. Explora y crea lienzos][ex9] | Colaboración | Utiliza Database Explorer y, después, crea y prueba un lienzo de clasificación asociado al repositorio |
| [10. Repaso y siguientes pasos][ex10] | Resumen | Repasa el flujo de trabajo, los recursos creados y otros materiales |

## Requisitos previos

Antes de participar en este taller, comprueba que tienes:

- [ ] Una cuenta de GitHub con un plan **Copilot Student, Pro, Pro+, Business o Enterprise** activo.
- [ ] Un equipo con **macOS, Linux o Windows**.
- [ ] [Git instalado][install-git] en tu equipo.

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye el agente, MCP, la revisión de código y las funciones de Copilot CLI que utiliza este taller; puedes completar todos los itinerarios con él.

> [!NOTE]
> Como la aplicación Copilot se ejecuta en tu equipo y no en un Codespace, el [ejercicio de requisitos previos][ex0] explica cómo instalar Node.js y crear una copia del proyecto antes de instalar la aplicación.

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva de la **aplicación GitHub Copilot**. Es una directiva independiente de la de Copilot CLI.

## Empieza

**[Empieza con los requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-app/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-canvases/
[ex10]: 10-review/
[install-git]: https://github.com/git-guides/install-git
[callout-student-plan-education]: https://github.com/education/students
