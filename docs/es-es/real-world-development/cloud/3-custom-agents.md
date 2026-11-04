---
title: "Ejercicio 3: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] son asistentes de IA especializados en tareas o ámbitos concretos del desarrollo. Sus archivos Markdown en `.github/agents` pueden incluir instrucciones, buenas prácticas, patrones de código y conocimiento del dominio. Así, los equipos pueden reutilizar su experiencia en agentes de accesibilidad, seguridad o pruebas siguiendo las Pautas de Accesibilidad para el Contenido Web (WCAG).

Los agentes se definen en archivos Markdown del proyecto, en `.github/agents`, o de forma global en `~/.copilot/agents`. Cada archivo tiene metadatos YAML con al menos `name` y `description`, seguidos de instrucciones que definen su comportamiento y especialidad.

### Diferencias entre los agentes personalizados y las habilidades

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] se definen principalmente con Markdown. Un agente personalizado es quien realiza el trabajo; las habilidades son herramientas que puede utilizar. El agente tiene su propia ventana de contexto y puede coordinar habilidades y otros agentes.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Pruébalo e itera para adaptarlo al entorno y al escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En este ejercicio:

- revisarás un agente personalizado de accesibilidad.
- asignarás una tarea al agente para implementar un modo de alto contraste.

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas. Comentarios recientes señalan que el tema oscuro resulta difícil de leer por el bajo contraste entre el texto y el fondo. El equipo de diseño solicita un modo de alto contraste que se pueda activar y desactivar.

## Revisa el agente de accesibilidad

Ya hay un agente personalizado para accesibilidad. Revisa sus instrucciones para saber cómo orientará a Copilot.

1. Abre `.github/agents/accessibility.md`.
2. Observa los campos `name` y `description` de los metadatos YAML.

> [!CAUTION]
> Los campos `name` y `description` de los metadatos son obligatorios para los agentes personalizados.

3. Revisa las secciones sobre responsabilidades, buenas prácticas, ejemplos de HTML, CSS y JavaScript, y errores habituales.

## Crea y asigna una incidencia

El panel de agentes es el centro para asignar tareas, supervisarlas y orientar el trabajo. Crea una incidencia de alto contraste y asígnala al agente personalizado.

1. Abre el repositorio en GitHub y selecciona **Issues**.
2. Selecciona **New issue** y, después, **Blank issue**.
3. En **Title**, escribe `Add high contrast mode to website`.
4. En **Description**, escribe:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

5. Selecciona **Create** y, en el lado derecho, **Assign to Copilot**.
6. Selecciona **Accessibility agent** en la lista de agentes personalizados.

   ![Captura de pantalla de la asignación del agente en la nube, con Accessibility resaltado en la selección del agente personalizado](../../../_images/ex5-select-custom-agent.png)

7. Selecciona **Assign**. Copilot empezará a trabajar en segundo plano.

## Resumen y pasos siguientes

Has:

- revisado cómo se definen los agentes personalizados.
- asignado una tarea al agente de accesibilidad para implementar el modo de alto contraste.

Continúa y [supervisa y orienta la sesión del agente desde el panel de agentes][next-lesson].

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para utilizar agentes personalizados][org-custom-agents]
- [Preparar la empresa para utilizar agentes personalizados][enterprise-custom-agents]

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
