---
title: "Ejercicio 2: Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El agente de GitHub Copilot en la nube puede resolver tareas en segundo plano y abrir una solicitud de incorporación de cambios de borrador para que una persona revise el resultado. En este ejercicio asignarás tareas de documentación y funcionalidades, y revisarás cómo prepara su entorno y trabaja.

En este ejercicio:

- personalizarás el entorno de desarrollo del agente.
- revisarás medidas para realizar operaciones de forma segura.
- aprenderás la importancia de definir con claridad el alcance de las incidencias.
- asignarás incidencias al agente.

## Escenarios

Tailspin Toys tiene deuda técnica: el código carece de comentarios TSDoc en funciones exportadas. Además, el equipo de diseño quiere explorar una sección de juegos relacionados en las páginas de detalles, con títulos de la misma categoría, para realizar pruebas de aceptación. Son tareas que pueden quedar relegadas y que el agente puede abordar de forma asíncrona.

## Acerca del agente en la nube

El [agente de GitHub Copilot en la nube][cloud-agent] trabaja en segundo plano. Puedes asignarle una incidencia de GitHub; el agente prepara el entorno, crea una solicitud de incorporación de cambios de borrador para registrar el progreso y comienza la tarea. Puedes consultar la sesión mientras trabaja o después. Cuando el cambio está listo para revisión, te menciona en la solicitud.

## Importancia de delimitar bien las instrucciones

No hay magia ni desaparece la necesidad de pensar. Define el alcance con cuidado, divide el trabajo en etapas y revisa el resultado como lo harías con el de otro desarrollador. Las bases del desarrollo de software no cambian al añadir IA generativa.

## Revisa las instrucciones existentes

Antes de asignar trabajo, examina en la interfaz web de GitHub o en un codespace:

- `.github/copilot-instructions.md`: revisa **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observa el campo `applyTo`, que aplica las instrucciones a archivos `**/*.test.ts`.

Al asignar la incidencia `Code lacks documentation`, comprueba si la solicitud de incorporación de cambios incluye comentarios TSDoc, convenciones de TypeScript y encabezados de comentarios.

## Entorno del agente en la nube

El agente utiliza [GitHub Actions][github-actions]. El flujo de trabajo de configuración especial, `.github/workflows/copilot-setup-steps.yml`, se ejecuta antes del trabajo para instalar las herramientas y dependencias necesarias. Este taller ya incluye la configuración de Node.js, dependencias del proyecto, navegadores para pruebas de extremo a extremo y la base de datos SQLite migrada y precargada.

El archivo de configuración incluye un único trabajo `copilot-setup-steps`. El disparador `workflow_dispatch` permite probarlo manualmente desde la pestaña **Actions**.

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos mínimos necesarios para *tus pasos*. Copilot recibirá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de la configuración, por ejemplo, para instalar dependencias, necesitarás el permiso `contents: read`. Si no lo clonas en estos pasos, Copilot lo hará automáticamente cuando terminen.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de frontend y aplicación: Node.js (ahora toda la aplicación utiliza Astro y Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga la base de datos SQLite local para que las compilaciones y pruebas dispongan de datos.
      - name: Set up the database
        run: npm run db:setup
```

## Asigna la tarea de documentación

La primera incidencia pedirá al agente que mejore la documentación del código y te permitirá observar la sesión mientras trabaja.

1. En una pestaña nueva, abre el repositorio en github.com y selecciona **Issues**.
2. Selecciona **New issue** y, después, **Blank issue**.
3. En **Title**, escribe `Code lacks documentation`.
4. En **Description**, escribe:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

5. Selecciona **Create** y, en el lado derecho, **Assign to Copilot**.

   ![Formulario de una incidencia de GitHub con la opción Assign to Copilot resaltada.](../../../_images/shared-assign-copilot.png)

6. Selecciona **Assign**.

   ![Detalles de asignación de Copilot en una incidencia.](../../../_images/ex4-assign-copilot-details.png)

7. Abre la pestaña **Pull Requests** y la solicitud nueva, cuyo título será similar a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la página.
8. Cuando aparezca la lista de tareas, revísala. Puede tardar varios minutos mientras Copilot prepara el entorno y analiza el proyecto.
9. En la cronología de la solicitud, comprueba que Copilot ha empezado a trabajar y selecciona **View session**. Si no aparece el estado actualizado, vuelve a cargar la página.

   ![Vista de la sesión de Copilot en la solicitud de incorporación de cambios.](../../../_images/ex4-view-session.png)

10. Observa cómo la sesión explora el código, analiza el estado del proyecto y crea cambios.

Mientras el agente trabaja, puedes asignarle otra tarea.

## Asigna una sección de juegos relacionados

Mientras el agente trabaja en la documentación, asigna una segunda tarea independiente para que pueda avanzar en paralelo.

1. En el repositorio, abre **Issues**, selecciona **New issue** y **Blank issue**.
2. En **Title**, escribe `Show related games on the game details page`.
3. En **Description**, escribe:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

4. Selecciona **Create** y, a la derecha, **Assign to Copilot**.

   ![Formulario de una incidencia de GitHub con la opción Assign to Copilot resaltada.](../../../_images/shared-assign-copilot.png)

5. Selecciona **Assign**. Un emoji de ojos 👀 en el primer comentario de la incidencia indica que Copilot está trabajando.

![Comentario de Copilot en una incidencia con el emoji de ojos que indica que el agente está trabajando.](../../../_images/ex4-issue-eyes-emoji.png)

El agente en la nube trabaja de forma asíncrona, por lo que no es necesario supervisarlo continuamente. Revisa su resultado cuando termine.

## Resumen y pasos siguientes

Has:

- preparado el entorno del agente para generar código.
- revisado cómo realizar operaciones de forma segura.
- comprobado la importancia de delimitar las incidencias.
- asignado incidencias al agente de Copilot.

Continúa y [crea y asigna una tarea a un agente personalizado][next-lesson]. El agente en la nube también puede utilizar servidores del protocolo de contexto del modelo (MCP) y las instrucciones personalizadas que has revisado en ejercicios anteriores.

## Recursos

- [Acerca del agente de GitHub Copilot en la nube][cloud-agent]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas para el flujo de configuración del agente en la nube][setup-workflow]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[github-actions]: https://docs.github.com/actions
