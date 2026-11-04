---
title: "Ejercicio 4: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] son asistentes de IA especializados en tareas o ámbitos de desarrollo. Se definen en archivos Markdown del directorio `.github/agents` del proyecto o en `~/.copilot/agents`. Cada archivo tiene metadatos YAML con `name` y `description`, seguidos de instrucciones sobre el comportamiento, la experiencia y las herramientas del agente.

La accesibilidad web se puede evaluar con las Pautas de Accesibilidad para el Contenido Web (WCAG).

### Diferencias entre los agentes personalizados y las habilidades

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] se definen principalmente con Markdown. Un agente personalizado realiza y coordina el trabajo; las habilidades son herramientas que puede utilizar. Por ejemplo, un agente de accesibilidad puede revisar y actualizar el sitio según las pautas de accesibilidad y utilizar habilidades para ejecutar pruebas.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Pruébalo e itera para adaptarlo a tu entorno y tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma sea accesible para todas las personas. El equipo de diseño solicita un modo de alto contraste que se pueda activar y desactivar y cuya preferencia se guarde en el almacenamiento local del navegador.

En este ejercicio:

- revisarás el agente personalizado de accesibilidad incluido en el proyecto.
- utilizarás ese agente en Copilot Chat para implementar un modo de alto contraste.

## Revisa el agente personalizado de accesibilidad

Empieza por comprobar cómo está definido el agente que utilizarás para la tarea de accesibilidad.

1. Vuelve al codespace y crea una rama nueva a partir de `main`:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abre `.github/agents/accessibility.md` y revisa los metadatos `name` y `description`.

> [!CAUTION]
> Los campos `name` y `description` de los metadatos son obligatorios para los agentes personalizados.

3. Revisa las responsabilidades, las buenas prácticas, los ejemplos de HTML, CSS y JavaScript, y los errores habituales.

## Usa el agente personalizado en Copilot Chat

VS Code muestra los agentes personalizados de `.github/agents` en el selector situado en la parte inferior de Copilot Chat.

1. Vuelve al codespace, abre Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva.
2. En la lista de agentes, selecciona **Agent** si aún no está seleccionado.
3. Abre el selector de agentes y elige **Accessibility agent**.

   ![Captura del selector de agentes de Copilot Chat.](../../../_images/shared-chat-mode-selector.png)
4. Envía este prompt:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Revisa las propuestas en línea y los archivos que el agente vaya modificando.

> [!NOTE]
> El proceso puede tardar varios minutos. El agente puede editar componentes Astro, CSS y pruebas.

## Resumen y pasos siguientes

Has:

- revisado el agente personalizado de accesibilidad.
- utilizado el agente en Copilot Chat para implementar un modo de alto contraste.

Continúa y [supervisa y orienta el trabajo del agente][next-lesson], revisando sus cambios y solicitando un modo claro en la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados de Awesome Copilot][awesome-copilot-agents]

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
