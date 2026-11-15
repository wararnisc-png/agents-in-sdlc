---
title: "Ejercicio 5 - Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

Cuando utilizas el modo de agente de GitHub Copilot, trabaja de forma autónoma: explora el código base, propone cambios, edita archivos y ejecuta comandos. Como trabaja en tu equipo en tiempo real, Copilot Chat en VS Code muestra las llamadas a herramientas y las ediciones de archivos a medida que se producen. Puedes revisar cada diff en línea, aceptar o rechazar cambios y orientar la conversación con mensajes de seguimiento para ajustar o ampliar el trabajo sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos en los archivos.
- pedirás al agente durante la sesión que añada un control para el modo claro, además del modo de alto contraste.

## Situación

El agente personalizado de accesibilidad del [ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño ha añadido una solicitud: también quiere un control para el modo claro, para los usuarios que prefieren un tema menos oscuro. En vez de iniciar una conversación nueva, ampliarás el trabajo en la sesión existente.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Cada edición aparece en línea en el chat, junto con un diff y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver cada llamada a herramientas. Verás lecturas y ediciones de archivos, además de los comandos de terminal que solicite ejecutar.
3. Cuando el agente proponga editar un archivo, aparecerá un diff en línea:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para revertirlo y dejar que el agente vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed** de la parte superior del chat para ver todos los archivos modificados por el agente durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta solicita permiso, por ejemplo, para ejecutar un comando del terminal, el agente se detendrá y mostrará una solicitud **Allow**. Aprueba solo los comandos con los que estés de acuerdo.

5. Espera a que el agente termine de implementar el modo de alto contraste. Verás un mensaje final que resume los cambios.

## Pide al agente que añada el modo claro

Ya está implementado el modo de alto contraste. Ahora ampliaremos la misma conversación con un control para el modo claro. Como continuarás en la misma sesión de chat, el agente conservará el contexto del trabajo anterior: los componentes que ha modificado, el enfoque de estilos y el uso del almacenamiento local.

1. Envía este mensaje de seguimiento en Copilot Chat:

    ```plaintext
    ¡Buen trabajo! Ahora añade un control para el modo claro junto al de alto contraste. El modo claro debe seguir el mismo patrón: guardarse en el almacenamiento local y estar disponible en la misma zona de la interfaz. El usuario debe poder activar de forma independiente el modo de alto contraste y el modo claro.
    ```

2. El agente continuará desde donde lo dejó, revisará los cambios realizados y propondrá cómo añadir el modo claro.
3. Revisa cada cambio nuevo a medida que aparezca, igual que con el modo de alto contraste. Usa **Keep** o **Undo** para cada diff.
4. Si el agente sigue un enfoque que no quieres —por ejemplo, intenta reorganizar la interfaz de los controles de una forma que no te gusta—, detenlo con el botón **Stop** junto al campo de mensaje y envíale una aclaración.

> [!TIP]
> Orientar una sesión en curso es más rápido que empezar de nuevo. Utiliza mensajes de seguimiento para pedir ajustes («simplifica el CSS: utiliza variables de CSS en lugar de repetir selectores»), corregir el enfoque («no añadas un tercer control; integra el modo claro en el panel de configuración existente») o ampliar el alcance («añade también métodos abreviados de teclado para ambos controles»).

## Revisa los cambios

Antes de confirmar el trabajo, revisa rápidamente todos los cambios realizados por el agente.

1. Abre la vista **Source Control** de VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en los componentes de Astro, los estilos y las pruebas relacionadas.
3. Abre algunos archivos modificados y revisa sus diffs. Confirma que se han aplicado las prácticas de accesibilidad del agente personalizado: atributos ARIA, navegación con el teclado, HTML semántico y almacenamiento local de las preferencias.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel Source Control. Los publicarás en [la lección siguiente][next-lesson].

## Resumen y siguientes pasos

Has utilizado el modo de agente de Copilot Chat para supervisar y dirigir una sesión en curso. Has revisado cada edición al aplicarse, aceptado o rechazado cambios y enviado mensajes de seguimiento para ampliar el trabajo sin perder el contexto.

En esta lección has explorado:

- supervisar el trabajo de un agente en tiempo real.
- aceptar y rechazar ediciones individuales.
- orientar una sesión en curso mediante mensajes de seguimiento.

En la [lección siguiente][next-lesson] publicarás el trabajo de accesibilidad en una solicitud de cambios y revisarás las modificaciones del agente personalizado local durante el laboratorio.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo de agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iteración sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
