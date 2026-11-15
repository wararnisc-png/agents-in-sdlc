---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Explora los modos de agente: utiliza Plan para acordar un enfoque, Autopilot para crear los filtros desde una incidencia e Interactive para revisar y verificar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Empezamos añadiendo una pequeña función al proyecto, pero los cambios más amplios requieren un proceso más completo. La aplicación GitHub Copilot está diseñada para adaptarse al flujo de trabajo de una organización y ayudarnos a crear lo adecuado de la forma correcta. Esta es la primera de varias lecciones en las que seguirás un proceso habitual de desarrollo dirigido por agentes: partirás de una incidencia para crear una función, comprobarás que el código es válido y se comporta como esperas y, por último, la combinarás correctamente con el proyecto.

> [!NOTE]
> Utilizarás la misma sesión durante todo el flujo de trabajo de la función. Normalmente se usarían sesiones o PR distintas para los diferentes tipos de archivo, pero vamos a simplificarlo para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una sesión de agente desde una incidencia de GitHub.
- definirás los requisitos en el modo **Plan**.
- implementarás la función con el modo **Autopilot**.
- revisarás el código.
- validarás manualmente la función en un lienzo de navegador.

Mientras sigues trabajando en esta función, actualizarás las instrucciones del repositorio, personalizarás la aptitud `quality-checks`, añadirás validación MCP, crearás un agente de QA y abrirás la PR de la función.

## Situación

El catálogo de Tailspin Toys está creciendo y sus visitantes necesitan filtrar los juegos por categoría y editorial. La incidencia de la lista de tareas describe la función, pero hay que acordar detalles como la combinación de categorías antes de programar. Utilizarás el modo Plan para resolver esas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Contexto

Incorporar agentes de programación con IA al flujo de desarrollo no cambia sus principios fundamentales. ¡De hecho, los hace aún más importantes! La mayoría de los desarrolladores siguen un proceso similar a este:

1. Abrir una incidencia que describa el trabajo pendiente.
2. Crear un plan con lo que hay que implementar.
3. Crear y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la función nueva.
6. Crear una solicitud de cambios (PR).
7. Combinar el código cuando se haya revisado y se hayan superado las comprobaciones de integración continua.

> [!NOTE]
> Los detalles concretos varían según el equipo y la organización, pero la mayoría de los procesos siguen alguna variante de este modelo.

Si sigues este enfoque estándar, te aseguras de que el código generado por IA cumple los requisitos y pasa por el mismo proceso de validación que el código escrito manualmente.

## Modos de sesión

El **modo de sesión** controla la autonomía del agente. Puedes seleccionarlo en el menú desplegable situado debajo del campo del mensaje y cambiarlo en cualquier momento:

- **Interactive:** tú y el agente trabajáis juntos. El agente propone cambios y espera tus indicaciones antes de continuar.
- **Plan:** el agente crea primero un plan. Revisas y apruebas el plan antes de que lo ejecute.
- **Autopilot:** el agente trabaja de forma autónoma: escribe código, ejecuta pruebas e itera sin esperar indicaciones.

Empieza en el modo Plan, revisa el plan y, después, usa Autopilot para implementarlo.

## Inicia una sesión desde la incidencia

Antes de empezar, confirma que la PR de las valoraciones con estrellas está combinada y que tu `main` local está actualizada.

1. En **Sessions**, selecciona la carpeta del repositorio Tailspin Toys y, después, **Issues** en la navegación superior. Abre **Allow users to filter games by category and publisher**. Es una incidencia existente creada a partir de la plantilla; no tienes que crear otra.
2. Selecciona **New session** y elige un **new working tree** basado en `main` actualizada.

    ![Vista de la incidencia en la aplicación GitHub Copilot con una flecha que señala el botón New session](../../../_images/app-new-session-from-issue.png)

3. Confirma que la incidencia está adjunta a la sesión y selecciona **Plan** en el selector de modo.

> [!NOTE]
> Si no se encuentra Node.js o npm, pide al agente que ejecute `node --version` y `npm --version`. Si funcionan en el terminal, pero no en la sesión, comprueba la variable `PATH` o la configuración del gestor de versiones de la aplicación y ciérrala completamente antes de volver a abrirla. Repite la operación y las comprobaciones que hayan fallado. No reinstales npm solo porque el agente no lo encuentre.

## Planifica la función de filtros

La planificación te permite revisar el enfoque antes de que Copilot escriba código. Como has iniciado la sesión desde la incidencia, Copilot ya dispone de la solicitud como contexto. Envía:

```plaintext
Implementa esta función.
```

Responde a las preguntas de Copilot y compara el plan con los criterios de aceptación de la incidencia. Comprueba que incluye filtros por categoría y editorial, controles accesibles, cambios en el acceso a datos y pruebas. Aclara cualquier comportamiento poco definido, como la combinación de varias categorías o qué ocurre cuando ningún juego coincide.

El plan debe incluir lint, pruebas unitarias, pruebas E2E y comprobación de tipos con las herramientas existentes del proyecto. Limita el trabajo a implementar y probar los filtros; crearás la PR después de completar el flujo de calidad. Solicita cambios al plan antes de aprobarlo y conserva la URL de la incidencia y las aclaraciones acordadas para validarlas más adelante.

## Aprueba Autopilot explícitamente

Cuando estés conforme con el plan, selecciona **Approve and implement this plan** o la opción equivalente de tu versión. Comprueba el modo activo en lugar de dar por hecho que la aprobación cambia el modo. Confirma que el indicador muestra **Autopilot**.

Copilot empezará a implementar la función. Observa cómo sigue el plan acordado, genera código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación de inmediato, así que revisa el plan antes. Si Copilot indica que faltan dependencias o que hay un conflicto de puertos, resuelve el problema de configuración antes de dar las comprobaciones por terminadas. Detén solo los servidores que hayas iniciado.

## Revisa y comprueba la implementación

Una vez generado el código, debes revisarlo antes de combinarlo, como harías con cualquier otro cambio. Revisemos el código y ejecutemos el sitio para comprobar que funciona correctamente.

1. Abre **Changes** e inspecciona la implementación de los filtros y las pruebas.
2. Compara el resultado con la incidencia y las aclaraciones aprobadas, incluidas las combinaciones de categorías y editoriales. Comprueba que los cambios siguen las instrucciones existentes del repositorio.
3. Revisa los resultados de lint, las pruebas unitarias, las pruebas E2E y la comprobación de tipos. Una comprobación omitida no cuenta como superada.
4. Resuelve los errores y vuelve a ejecutar las comprobaciones afectadas antes de aceptar la implementación. La configuración E2E de Playwright compila y sirve una vista previa y puede reutilizar un servidor local; comprueba que el servidor probado pertenece a este árbol de trabajo, no a una lección anterior.

## Explora la nueva función

El código parece correcto, pero ¿se ejecuta? Iniciemos la aplicación como antes y abramos el sitio en un lienzo de navegador.

1. Envía este mensaje para pedir a Copilot que inicie la aplicación y abra la página en el lienzo:

    ```plaintext
    Inicia la aplicación y ábrela en el lienzo del navegador.
    ```

2. En unos instantes, la aplicación se iniciará y se abrirá una ventana del navegador dentro de la aplicación Copilot.
3. Selecciona una categoría y confirma que los resultados coinciden. Quita el filtro y, después, selecciona una editorial y comprueba los resultados.
4. Combina filtros de categoría y editorial y compara los resultados con la incidencia y el plan aprobado. Si se admiten varias categorías, comprueba que se combinan de la forma acordada.
5. Prueba una combinación sin juegos coincidentes y revisa el estado vacío. Quita o restablece los filtros y confirma que vuelve a aparecer la lista completa.
6. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado en esta sesión y cierre el lienzo:

    ```plaintext
    Detén el servidor de desarrollo y cierra el lienzo del navegador.
    ```

## Conserva esta sesión para las lecciones siguientes

Todavía no crees ni combines la PR de los filtros. Conserva esta sesión, este árbol de trabajo y esta rama para las lecciones 4 a 8. En la siguiente lección aplicarás instrucciones personalizadas al código de los filtros y, después, añadirás la aptitud y las mejoras de QA antes de crear y combinar la PR conjunta en la lección 8. Puedes dejar la sesión inactiva después de detener el servidor de desarrollo y volver a ella para la lección siguiente.

## Resumen y siguientes pasos

Has utilizado distintos modos de agente para crear y revisar una función. En esta lección:

- has iniciado una sesión de agente desde una incidencia de GitHub.
- has definido los requisitos en el modo **Plan**.
- has implementado la función con el modo **Autopilot**.
- has revisado el código.
- has validado manualmente la función en un lienzo de navegador.

A continuación, profundizarás en cómo se genera el código y te asegurarás de que siga las prácticas documentadas mediante el [uso de instrucciones personalizadas][next-lesson].

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
