---
title: "Lección 8 - Crea y combina la PR de la funcionalidad"
description: "Revisa los filtros, las instrucciones, la aptitud actualizada, el perfil de QA y las pruebas; después, autoriza a Agent Merge a crear y combinar la PR."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación de los filtros, las actualizaciones de instrucciones y de la aptitud, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Es el momento de revisarlos juntos y abrir una solicitud de cambios. Combinaste personalmente la PR de las valoraciones con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo normal sería separar la función, las actualizaciones de instrucciones y de la aptitud, y el agente de QA en varias PR. Para simplificar el taller, has mantenido todo el flujo de filtros y calidad en una misma sesión y rama, y lo incluirás en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- inspeccionarás la PR completa de la función y las pruebas de verificación.
- autorizarás a Agent Merge solo después de revisar los cambios y confirmar que la PR se ha combinado.

## Situación

Durante el flujo de filtros, has utilizado Copilot para planificar, implementar y verificar una función. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR, pero mantener bajo el control del desarrollador la autorización para combinarla.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una solicitud de cambios a través de la aplicación GitHub Copilot. Al activarlo, la sesión de la aplicación lee la solicitud y resuelve sus bloqueos: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y vuelve a aplicar los cambios cuando sea necesario. Después, combina la solicitud en cuanto GitHub lo permite. Se ejecuta en segundo plano, sigue funcionando aunque se reinicie la aplicación y se desactiva cuando la PR se combina.

Hasta ahora has seleccionado **Merge pull request** personalmente. Agent Merge puede encargarse de esa tarea, pero su capacidad de editar código y combinar la PR sigue requiriendo tu autorización explícita. Antes de conceder permiso para combinar, revisa las acciones que tiene permitidas y el trabajo realizado.

## Utiliza Agent Merge para gestionar la PR

Ya has creado y revisado todo el código. Ahora dejaremos que Agent Merge gestione el proceso de la PR.

1. Utiliza el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El botón cambiará a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Seleccionar la opción del menú desplegable no lo inicia.

Se iniciará el proceso de Agent Merge. El agente:

- creará la solicitud de cambios con un título y una descripción.
- incluirá en la descripción una referencia a la incidencia relacionada si has iniciado la sesión desde una incidencia.
- volverá a aplicar los cambios sobre la rama de destino o resolverá posibles conflictos.
- supervisará el proceso de integración continua para comprobar que se superan todas las comprobaciones.
- supervisará la PR para detectar comentarios de otros desarrolladores o de la revisión de código de Copilot y hará los cambios necesarios para resolverlos.
- podrá combinar automáticamente la PR cuando todo se haya completado correctamente.

Permitiremos que Agent Merge combine la PR cuando se hayan superado todas las comprobaciones.

5. Revisa el diff de la PR y las pruebas de verificación antes de conceder permiso para combinar.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que **Merge pull request** está marcado.
8. Pide explícitamente al agente que combine la PR:

    ```plaintext
    Combina la PR cuando se hayan superado todas las comprobaciones y aprobaciones obligatorias. No omitas las protecciones del repositorio.
    ```

9. Supervisa el progreso y resuelve cualquier bloqueo que indique. Antes de continuar, comprueba que el estado de la PR es **Merged**; que el permiso para combinar esté habilitado o que haya un agente trabajando no confirma que la PR se haya combinado.

> [!IMPORTANT]
> Agent Merge no omite las protecciones del repositorio ni los permisos que falten. Resuelve esos bloqueos antes de continuar.

## Resumen y siguientes pasos

Has automatizado varios pasos del proceso de desarrollo: generación de código, pruebas y validación y, ahora, gestión de solicitudes de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una PR.
- has inspeccionado la PR completa de la función y las pruebas de verificación.
- has autorizado a Agent Merge solo después de revisar el trabajo y has confirmado que la PR se ha combinado.

A continuación, [utilizarás un lienzo existente y crearás uno de clasificación][next-lesson] para explorar una forma más completa de examinar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Gestión de incidencias y solicitudes de cambios con la aplicación GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
