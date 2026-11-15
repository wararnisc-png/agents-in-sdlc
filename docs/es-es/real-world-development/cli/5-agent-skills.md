---
title: "Lección 5 - Personaliza y utiliza la aptitud quality-checks"
description: "Explora la aptitud quality-checks existente, personaliza el formato de su informe y úsala para validar los filtros."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Programar no consiste solo en escribir código. Ya hemos comprobado manualmente que el código funciona y hemos utilizado archivos de instrucciones para asegurarnos de que sigue nuestros estándares. ¿Qué ocurre con las pruebas, lint y los demás aspectos de la integración continua (CI)?

Las **aptitudes de agente** son adecuadas para estas tareas. Ayudan a Copilot a entender cómo debe ejecutar operaciones como estas.

En esta lección:

- explorarás la aptitud `quality-checks` existente.
- personalizarás el formato de los resultados.
- volverás a cargar la aptitud y la ejecutarás.

## Situación

Tailspin Toys utiliza la aptitud `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las aptitudes de agente agrupan instrucciones reutilizables para tareas, scripts ejecutables y recursos auxiliares que el agente carga cuando los necesita. En esencia, son carpetas que contienen un archivo Markdown llamado `SKILL.md`. El archivo incluye un frontmatter con el nombre y la descripción de la aptitud, una explicación de su funcionamiento y directrices sobre cuándo debe utilizarse. La carpeta también puede incluir subcarpetas con scripts y otros recursos que la aptitud necesite.

> [!NOTE]
> Las subcarpetas y los archivos adicionales son opcionales. La aptitud `quality-checks` de Tailspin Toys solo contiene `SKILL.md` porque utiliza los comandos existentes del proyecto.

Las aptitudes pueden ubicarse en `.github/skills` para compartirlas y reutilizarlas en el equipo, o en la carpeta de aptitudes del usuario `~/.copilot/skills`.

## Explora la aptitud

Vamos a explorar la aptitud que ha creado el equipo de Tailspin Toys para ejecutar pruebas unitarias, lint y comprobaciones de tipos: `quality-checks`.

1. Vuelve a tu Codespace. En el editor de Codespaces, abre `.github/skills/quality-checks/SKILL.md`.
2. Lee el campo `name` y la descripción de la parte superior. La descripción ayuda a Copilot a saber cuándo debe utilizar la aptitud.
3. Lee las instrucciones y fíjate en cómo guían a Copilot para ejecutar las pruebas y lint.
4. Observa que todavía no hay una sección **Results output formatting**.

## Ejecuta la aptitud antes de hacer cambios

Puedes invocar aptitudes directamente desde Copilot CLI o utilizar lenguaje natural. Pidamos a Copilot que ejecute las tres comprobaciones de la aptitud.

1. Vuelve a la conversación de los filtros en el modo Interactive.
2. Envía este mensaje:

   ```plaintext
   Ejecuta la aptitud quality-checks para las pruebas unitarias, lint y las comprobaciones de tipos.
   ```

3. Lee el informe final.

## Personaliza el informe

Queremos mejorar el informe para que indique qué se ha ejecutado, si ha terminado correctamente y qué resultados han devuelto las herramientas. Actualizaremos la aptitud para que genere ese informe.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade esta sección al final del archivo:

   ```markdown
   ## Formato de los resultados

   Al terminar, indica cada comando ejecutado y si se ha superado, ha fallado o ha quedado bloqueado. Incluye el número de pruebas, la duración, los errores, las advertencias y otras métricas solo cuando la herramienta las proporcione. Indica el siguiente paso ante cualquier error o bloqueo y nunca presentes una comprobación omitida o incompleta como superada.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la aptitud actualizada

Ya has hecho el cambio; ahora vamos a probarlo. Copilot CLI puede volver a cargar las aptitudes editadas sin reiniciar la conversación.

1. Escribe:

   ```plaintext
   /skills reload
   ```

2. Envía exactamente el mismo mensaje que antes:

   ```plaintext
   Ejecuta la aptitud quality-checks para las pruebas unitarias, lint y las comprobaciones de tipos.
   ```

3. Lee el informe final y compáralo con el primero.

## Resumen y siguientes pasos

Has personalizado y utilizado una aptitud de agente existente. En esta lección:

- has explorado la aptitud `quality-checks` para pruebas unitarias, lint y comprobaciones de tipos.
- has personalizado el formato de los resultados.
- has vuelto a cargar y ejecutado la aptitud.

Este cambio se incluirá con los filtros en la PR de la función. A continuación, permitirás que Copilot interactúe directamente con el sitio [mediante el servidor Playwright MCP][next-lesson].

## Otros ejemplos de aptitudes

Estos ejemplos de la comunidad sirven de referencia; no tienes que completarlos:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de trabajo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y script de exportación incluido: `drawio`][drawio-example]
- [Pruebas del navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
