---
title: "Lección 8 - Crea y combina la PR de la funcionalidad"
description: "Revisa los filtros, las instrucciones, la aptitud actualizada, el perfil de QA y las pruebas; después crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación de los filtros, las actualizaciones de instrucciones, la aptitud actualizada, el perfil de control de calidad (QA) y las pruebas están guardados en una misma rama. Ahora toca revisarlos en conjunto y abrir una solicitud de cambios. Combinaste manualmente la PR de la valoración con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo normal sería separar la funcionalidad, las actualizaciones de instrucciones, la aptitud y el agente de QA en varias PR. Para simplificar el taller, has mantenido todo el flujo de calidad y filtros en una misma conversación y rama, y lo incluirás en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- inspeccionarás el cambio completo de la funcionalidad y las pruebas de verificación.
- crearás la PR de los filtros.
- activarás Agent Merge solo después de la revisión y confirmarás que la PR se ha combinado.

## Situación

Durante el flujo de trabajo de los filtros, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR, pero mantener el control del desarrollador sobre la autorización de la combinación.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de cambios. Al activarlo, Copilot resuelve los bloqueos de la PR —corrige errores en las comprobaciones de integración continua (CI), responde a comentarios de revisión y vuelve a aplicar los cambios cuando sea necesario— y, después, activa la combinación automática de GitHub si el repositorio lo permite.

Hasta ahora has seleccionado **Merge pull request** manualmente. Agent Merge puede encargarse de esa tarea. Revisa el trabajo y confirma que está listo antes de activarlo.

## Usa Agent Merge para gestionar la PR

Ya has creado todo el código. Vamos a revisarlo, crear la PR y dejar que Agent Merge gestione el resto.

1. Vuelve a tu Codespace.
2. Abre el diálogo de agentes escribiendo `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR nueva con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua en la PR. Cuando todas las comprobaciones se superen, combinará la PR.
7. Confirma que Copilot muestra un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, lee el motivo que indica y completa manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y siguientes pasos

Has automatizado varios pasos del proceso de desarrollo: generación de código, pruebas y validación, y ahora la gestión de solicitudes de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- has inspeccionado el cambio completo de la funcionalidad y las pruebas de verificación.
- has creado la PR de los filtros.
- has activado Agent Merge solo después de la revisión y has confirmado que la PR se ha combinado.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para gestionar el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

## Recursos

- [Gestión de solicitudes de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
