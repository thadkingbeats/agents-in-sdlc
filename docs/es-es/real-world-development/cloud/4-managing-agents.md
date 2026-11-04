---
title: "Ejercicio 4: Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los ejercicios anteriores has pedido al agente de GitHub Copilot en la nube que realice tres tareas para mejorar la experiencia de usuario. Aunque trabaja de forma autónoma y asíncrona, es importante supervisar estas tareas.

La [página de agentes][agents-page] de GitHub.com permite revisar las tareas con solicitudes de incorporación de cambios abiertas, consultar las operaciones realizadas y orientar una sesión activa.

En este ejercicio:

- explorarás la página de agentes para supervisar tareas.
- orientarás una sesión activa para solicitar otra funcionalidad.

## Escenario

Después de asignar el modo de alto contraste, el equipo decide añadir también un modo claro. Como el agente ya está modificando los estilos y los controles, puedes pedirle que incorpore ese cambio a la tarea en curso.

## Revisa las tareas del agente

La página de agentes permite consultar las sesiones que has iniciado y las operaciones que realiza Copilot.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa las tareas en los paneles principal e izquierdo. Deberías ver las tareas que asignaste, como documentar el código, generar API para modificar juegos y añadir el modo de alto contraste.
3. Selecciona una tarea en curso y revisa sus operaciones, por ejemplo, la obtención del código, la preparación del entorno, la configuración de servidores del protocolo de contexto del modelo (MCP) y la implementación.
4. Revisa también el panel de solicitudes de incorporación de cambios de la derecha, donde se muestran la solicitud y los archivos modificados.

Los pasos exactos varían según el estado del trabajo y el enfoque que haya seguido Copilot.

## Orienta al agente en la nube

Ahora añadirás el modo claro a la sesión que ya trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título puede variar según el nombre que Copilot haya asignado y el estado del trabajo.

   ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Espera a que termine la configuración y empiece el trabajo.
3. En el cuadro **Steer active session while Copilot is working**, escribe:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Tarea del agente en la nube en la página de agentes, con el cuadro para orientar la sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Comprueba que Copilot lo reconoce y lo incorpora al trabajo.

## Deja que Copilot trabaje

Copilot incluirá la nueva solicitud al terminar el paso que esté realizando. El proceso puede tardar varios minutos.

## Resumen y pasos siguientes

Has:

- explorado la página de agentes para supervisar las tareas del agente en la nube.
- orientado una sesión activa para solicitar otra funcionalidad.

Continúa y [itera sobre las solicitudes de incorporación de cambios de Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
