---
title: "Ejercicio 2 - Añade funciones con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas de una aplicación suelen afectar a varios archivos y requieren otras tareas, como ejecutar pruebas. El proceso de desarrollo suele incluir localizar todos los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo se ha pasado por alto y volver a actualizarlo. Y la lista continúa.

El modo de agente de Copilot puede ayudarte con este trabajo.

El modo de agente de Copilot está diseñado para trabajar de forma más autónoma en el IDE. Se comporta de manera parecida a un desarrollador: primero explora la estructura del proyecto, realiza los cambios necesarios, ejecuta tareas como las pruebas y corrige automáticamente los errores que encuentra. Vamos a ver cómo utilizar el modo de agente para añadir funciones al sitio.

> [!NOTE]
> Aunque los nombres se parecen, el modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el IDE y permite ciclos de respuesta rápidos e interacción continua. El agente en la nube trabaja de forma asíncrona, como un miembro del equipo, y se comunica contigo mediante incidencias y solicitudes de cambios.

En este ejercicio aprenderás a:

- utilizar el modo de agente de Copilot para explorar el proyecto, identificar los archivos pertinentes y coordinar cambios.
- implementar funciones en la interfaz de usuario y la capa de datos.
- revisar los cambios y las pruebas generados por el modo de agente antes de combinarlos con el código.

## Situación

El catálogo de juegos sigue creciendo y quieres que los usuarios puedan filtrarlos por categoría y editorial. En el ejercicio anterior ya has añadido un asistente de editoriales. Ahora completarás el trabajo pendiente de la capa de datos, la interfaz de usuario y las pruebas con el modo de agente de Copilot.

## Ejecuta el sitio web de Tailspin Toys

Antes de hacer cambios, exploremos el sitio web de Tailspin Toys para conocer sus funciones actuales.

El sitio es una plataforma de financiación colectiva para juegos de mesa con temática de desarrollo. Permite mostrar una lista de juegos y sus detalles. Toda la aplicación está desarrollada con Astro y genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM en el frontmatter; no hay una API de backend independiente ni un framework de interfaz de usuario del lado del cliente. Los asistentes reutilizables de acceso a datos se encuentran en `src/lib/`, y la interactividad se implementa con un pequeño `<script>` de Astro específico que utiliza las API estándar del DOM.

### Inicia el sitio

Para facilitar la ejecución del sitio, el comando `npm run dev` inicia un único servidor de desarrollo de Astro. Puedes ejecutarlo en GitHub Codespaces así:

1. Vuelve a tu Codespace. Después del ejercicio anterior, deberías estar en `main`.
2. Abre un terminal en el Codespace con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea y selecciona una rama nueva para este trabajo de filtros:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio con el siguiente comando:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, verás un mensaje parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si se abre un diálogo que te pregunta si quieres abrir un navegador en `http://localhost:4321`, ciérralo seleccionando **x**.

5. Mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona la dirección del servidor Astro, `http://localhost:4321`, en el terminal.

> [!NOTE]
> En Codespaces, al seleccionar el enlace local en el terminal se te redirigirá automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Es un túnel privado al Codespace, que ahora aloja el servidor web.

### Explora el sitio

Cuando el sitio esté en ejecución, podrás explorar sus funciones principales:

- **Página de inicio:** muestra una lista de juegos de mesa con sus títulos, imágenes y descripciones.
- **Página de detalles del juego:** al seleccionar un juego, se abre una página con más información, como el título, la descripción, la editorial y la categoría.

## Explora la lista de tareas con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los ejercicios siguientes, vuelve a tu Codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. La elección del modo y del modelo varía según el ejercicio; cada paso lo indicará cuando sea pertinente.

La implementación inicial del sitio funciona, pero queremos ampliarla con nuevas funciones. Empezaremos revisando la lista de tareas. Al crear el proyecto a partir de la plantilla, se generó automáticamente una lista de incidencias; pide a GitHub Copilot que te las muestre.

1. Selecciona **Agent** en el selector de agentes de la vista Chat. El agente puede planificar e implementar cambios de forma autónoma en varios archivos, ejecutar comandos del terminal e invocar herramientas.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no manifiestan preferencia por un modelo concreto. Durante su desarrollo utilizamos Claude Sonnet 4.5, por lo que lo incluimos en estas instrucciones. Así esperamos que las sugerencias de código sean relativamente coherentes y la experiencia sea más uniforme. Sin embargo, como los modelos de lenguaje grandes (LLM) son probabilísticos, puede que las sugerencias que recibas sean distintas a las que se describen en el taller. Es normal y esperable.

> [!NOTE]
> Debido al carácter probabilístico de los LLM, Copilot puede utilizar otro comando MCP, pero debería poder completar la tarea.

3. Pide a Copilot que consulte las incidencias pendientes con este mensaje:

   ```plaintext
   Muéstrame la lista de tareas pendientes del repositorio de GitHub. Ayúdame a priorizarlas según su utilidad para los usuarios.
   ```

4. Selecciona **Continue** para ejecutar el comando que enumera todas las incidencias.
5. Revisa la lista de incidencias que genera Copilot.

Observa que Copilot también ha priorizado las incidencias según lo que considera más útil para los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere código, revisa el archivo de instrucciones que proporcionará contexto a Copilot. Utilizarás el archivo de la [interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que contiene información sobre cómo añadir funciones al sitio.

1. En tu Codespace, abre `.github/instructions/ui.instructions.md`.
2. Fíjate en las directrices generales para añadir funciones, que incluyen:
   - una descripción general de la arquitectura.
   - principios de diseño de componentes, capacidad de prueba y accesibilidad.
   - enlaces a archivos de instrucciones para tipos de archivos concretos, como:
     - Astro.
     - Tailwind CSS.
     - Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden incluir referencias a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas a la ubicación del archivo de instrucciones. Así se pueden reutilizar las instrucciones, dividir conjuntos complejos en partes pequeñas y manejables, y proporcionar ejemplos y plantillas.

## Implementa los filtros

Para completar los filtros hay que realizar al menos tres cambios distintos en la aplicación:

- añadir o ajustar la lógica de filtros restante en la capa de datos (`src/lib/`).
- añadir o actualizar las pruebas del comportamiento de los filtros.
- actualizar la página con la lista de juegos para incluir la interfaz de filtros.

Además, hay que ejecutar las pruebas y comprobar que se superan antes de combinar los cambios. El modo de agente de Copilot puede realizar estas tareas. Vamos a añadir la funcionalidad.

1. Puedes continuar con la conversación actual de Copilot o seleccionar **New Chat** para iniciar otra.
2. Selecciona **Add Context**, **Instructions** y **ui** como archivo de instrucciones.

   ![Captura en la que se selecciona el archivo de instrucciones de la interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Comprueba que **Agent** sigue seleccionado en el selector de agentes de la vista Chat.

   ![Captura del selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Comprueba que **Claude Sonnet 4.5** sigue seleccionado como modelo.
5. Pide a Copilot que implemente la funcionalidad según la incidencia relacionada de la lista de tareas:

   ```plaintext
   Actualiza el sitio para incluir filtros por editorial y categoría según los requisitos de la incidencia relacionada de GitHub. Ya existe un asistente de editoriales del ejercicio anterior; consérvalo y ajústalo si hace falta al completar el trabajo restante de la capa de datos, la interfaz y las pruebas. Comprueba que todas las pruebas se superan antes de terminar. El servidor ya está en ejecución, no hace falta iniciarlo.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos relacionados con la funcionalidad: los asistentes de la capa de datos, la interfaz de usuario y las pruebas. Después, modifica los archivos y ejecuta las pruebas.

   ![Captura en la que Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar varios minutos, según la complejidad de la tarea y del código base. Durante este proceso, quizá aparezcan los botones **Keep** y **Undo** en el editor. Al terminar, podrás conservar o deshacer todos los cambios; no tienes que seleccionar estos botones mientras Copilot trabaja.

7. Cuando Copilot te lo pida, selecciona **Continue** para ejecutar las pruebas.

   ![Captura de un diálogo de Copilot Chat que pide permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Es posible que haya pausas e incluso que algunas pruebas fallen durante el proceso. No pasa nada: Copilot alterna entre la generación de código y las pruebas hasta completar la tarea y dejar de detectar errores.

   ![Captura de una sesión completa de Copilot Chat con el modo de agente](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explora el código generado para detectar posibles problemas.

> [!CAUTION]
> Recuerda que siempre es importante revisar el código que genera Copilot o cualquier otra herramienta de IA.

10. Vuelve al navegador con el sitio en ejecución y explora la funcionalidad nueva.
11. Cuando hayas confirmado que todo funciona y revisado el código, selecciona **Keep** en la ventana de Copilot Chat.

## Resumen y siguientes pasos

¡Enhorabuena! En este ejercicio has aprendido a utilizar el modo de agente de GitHub Copilot para añadir funciones al sitio de Tailspin Toys. Has aprendido a:

- implementar funciones en la interfaz de usuario y la capa de datos con el modo de agente de GitHub Copilot.
- utilizar el modo de agente para explorar el proyecto, identificar los archivos pertinentes y coordinar cambios.
- revisar los cambios y las pruebas generados por el modo de agente antes de combinarlos con el código.

Ahora [probaremos la funcionalidad con el servidor Playwright MCP][next-lesson] y crearemos una solicitud de cambios.

### Ejercicio de exploración adicional: implementa la paginación

Al crecer la lista de juegos, será necesario habilitar la paginación. Aplica lo aprendido en este ejercicio y pide a Copilot que añada paginación al sitio. Al planificar el código:

- sigue las prácticas recomendadas existentes, incluidos los archivos de instrucciones.
- decide cómo quieres implementar la paginación: por ejemplo, si los usuarios podrán elegir el tamaño de página o si será fijo.
- proporciona a Copilot las instrucciones necesarias para generar la implementación que necesitas.
- itera con GitHub Copilot, pide cambios y añade contexto. Así suele trabajarse con Copilot.

## Recursos

- [Modos ask, edit y agent de Copilot: qué hacen y cuándo se utilizan][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
