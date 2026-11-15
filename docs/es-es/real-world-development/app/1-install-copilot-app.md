---
title: "Lección 1 - Instala la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio que has creado a partir de la plantilla, familiarízate con el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La [**aplicación GitHub Copilot**][about-copilot-app] es una aplicación de escritorio para el desarrollo dirigido por agentes. Se basa en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que los repositorios, las ramas y las canalizaciones de CI funcionan sin configuración adicional. Está diseñada para flujos de trabajo en los que diriges varios agentes en paralelo —cada uno en su propio espacio de trabajo aislado— en lugar de hacer todo el trabajo por tu cuenta, y automatizas tareas repetitivas. Ya tienes Node.js instalado y una copia del proyecto preparada; ahora instalarás la aplicación y conectarás el repositorio.

En esta lección:

- instalarás la aplicación GitHub Copilot e iniciarás sesión.
- añadirás el proyecto a la aplicación desde su repositorio de GitHub.
- conocerás el espacio de trabajo, incluida la lista de tareas que la plantilla ha preparado.
- probarás un chat rápido para conocer la propia aplicación.

## Situación

Tu equipo está adoptando agentes de IA para abordar una lista de tareas cada vez mayor. La aplicación Copilot ofrece un único lugar desde el que dirigir ese trabajo: seleccionar incidencias, ejecutar agentes, revisar cambios y combinar solicitudes de cambios. En esta lección instalarás y conectarás la aplicación, y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Se requiere un plan de Copilot válido: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva de la **aplicación GitHub Copilot**.

## Instala y configura la aplicación GitHub Copilot

El primer paso para utilizar la aplicación GitHub Copilot es instalarla. Hay versiones para Windows, macOS y Linux. Vamos a instalar la aplicación, autenticarte y añadir el repositorio Tailspin Toys.

1. En un navegador, abre la [página de inicio de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación después de instalarla.
4. Selecciona **Sign in to GitHub** y sigue las instrucciones para iniciar sesión con una cuenta de GitHub.com o GHE.com. Si utilizas GitHub Enterprise Cloud con residencia de datos, elige **GitHub Enterprise Cloud** e introduce el nombre de host `*.ghe.com` cuando se te solicite.

   Si utilizas GitHub Enterprise Server, completa primero la incorporación con tu cuenta en la nube. Después, abre **Settings**, selecciona **Accounts**, selecciona **Add account** y elige **GitHub Enterprise Server**. Sigue las instrucciones para autorizar la aplicación en el navegador, como se describe en la [guía de inicio de sesión en Enterprise Server][ghes-sign-in].

5. Si durante la incorporación se te ofrece seleccionar repositorios, elige el repositorio de Tailspin Toys que has creado a partir de la plantilla. También puedes omitir este paso y añadir el proyecto más adelante.
6. Cuando se te solicite, elige un tema y completa la incorporación.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no es necesario volver a añadirlo.
8. Si todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Indica el propietario y el nombre del repositorio que anotaste en los requisitos previos.
9. Comprueba que el repositorio aparece en la barra lateral. En esta organización, las carpetas de repositorio, como `tailspin-toys`, aparecen agrupadas en **Sessions**, y las sesiones individuales se muestran debajo de cada repositorio.

## Familiarízate con el espacio de trabajo

Con el proyecto conectado, dedica un momento a explorar el espacio de trabajo. La aplicación organiza el contenido en varias áreas de la barra lateral:

- **New:** aquí puedes iniciar una sesión de chat nueva con Copilot.
- **Pull requests:** muestra las solicitudes de cambios mediante la integración nativa con GitHub. Desde aquí puedes explorarlas y filtrarlas, comprobar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues:** muestra las incidencias de la misma forma. Puedes explorarlas y filtrarlas, e iniciar una sesión desde una incidencia.
- **Automations:** tareas de agente guardadas que se ejecutan según una programación o bajo demanda. Sirven para gestionar listas de tareas, realizar el mantenimiento periódico del proyecto u ocuparse de otras tareas rutinarias. El resumen final las presenta como un siguiente paso, no como otro ejercicio del taller.
- **Customize:** permite añadir funciones a la aplicación Copilot mediante servidores MCP, complementos, aptitudes y otros componentes. La utilizarás para configurar Playwright MCP.
- **Chats:** conversaciones breves para consultas y lluvias de ideas que no necesitan una rama ni un espacio de trabajo propios. Esta sección aparece después de iniciar el primer chat. Si no está visible, selecciona **+** junto a **Sessions** para iniciar un chat.
- **Sessions:** agrupa las carpetas de repositorio y las sesiones de agente. Selecciona el nombre de un repositorio, como `tailspin-toys`, para abrir su vista, o selecciona una sesión debajo para volver a la conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado, así que puedes ejecutar varias a la vez sin que sus cambios entren en conflicto. Iniciarás tu primera sesión cuando añadas las valoraciones con estrellas.

Explorarás el espacio de trabajo durante el taller.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si es posible, puede ayudarte a orientarte.

### Localiza la lista de tareas preparada

Es probable que casi todos los proyectos tengan tareas pendientes, y Tailspin Toys no es una excepción. Vamos a explorar la lista de incidencias que se creó al generar el proyecto a partir de la plantilla.

1. En **Sessions**, selecciona la carpeta del repositorio Tailspin Toys, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título, sin dar por hecho su número:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia y lee sus detalles. Cada incidencia también sirve como punto de partida para una sesión de agente. Después de hacer un primer cambio rápido, partirás de la incidencia de filtros.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar solo elementos de los repositorios que has añadido a la aplicación Copilot. Para ver tareas de otros repositorios, añádelos a la aplicación.

## Prueba un chat rápido

Una buena forma de familiarizarte con la aplicación es utilizarla para conocer la *propia aplicación*. Para eso sirve el **chat rápido**. Permite hacer una pregunta o plantear ideas sin crear una rama ni un árbol de trabajo, por lo que resulta adecuado para consultas rápidas y puntuales que no necesitan una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat. Si **Chats** todavía no está visible, selecciona **+** junto a **Sessions** para iniciar el primer chat. Después aparecerá **Chats**.
2. Pregunta cómo funcionan las sesiones de la aplicación:

   ```plaintext
   ¿Cómo utiliza los árboles de trabajo la aplicación GitHub Copilot?
   ```

3. Lee la respuesta en la vista de conversación. Verás que cada sesión se ejecuta en su propio árbol de trabajo de Git aislado, lo que permite ejecutar varios agentes en paralelo sin que sus cambios entren en conflicto. Puedes continuar la conversación o iniciar otra cuando quieras.

## Resumen y siguientes pasos

¡Enhorabuena! Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub.
- añadir un proyecto desde su repositorio de GitHub.
- familiarizarte con el espacio de trabajo y localizar la lista de tareas inicial en **Issues**.
- utilizar un chat rápido para formular una pregunta breve y puntual.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] para mostrar una valoración con estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Introducción a la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
[ghes-sign-in]: https://docs.github.com/enterprise-server@3.22/copilot/copilot-on-ghes/sign-in-on-copilot-app
