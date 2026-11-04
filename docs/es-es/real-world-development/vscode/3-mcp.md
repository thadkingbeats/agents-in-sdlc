---
title: "Ejercicio 3: Prueba la funcionalidad con el servidor Playwright MCP"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Has creado los filtros con el modo de agente. Antes de abrir una solicitud de incorporación de cambios, comprueba que funcionan en el navegador. Configura el servidor Playwright MCP para que Copilot pueda controlar un navegador y probar la funcionalidad.

En este ejercicio:

- conocerás el protocolo Model Context Protocol (MCP) y cómo amplía las herramientas de Copilot.
- añadirás el servidor Playwright MCP al espacio de trabajo.
- pedirás a Copilot que pruebe manualmente los filtros en un navegador.
- publicarás la rama y abrirás una solicitud de incorporación de cambios.

## ¿Qué es Model Context Protocol?

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos. Un servidor MCP actúa como puente y proporciona acceso a recursos y herramientas.

![Diagrama del modo de agente y su interacción con el contexto, el modelo de lenguaje y las herramientas, incluidas las que proporcionan los servidores MCP y las extensiones de VS Code.](../../../_images/ex1-mcp-diagram.png)

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)** proporciona acceso a interfaces de programación de aplicaciones (API) para gestionar repositorios, incidencias y solicitudes de incorporación de cambios.
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)** automatiza un navegador con Playwright.

GitHub mantiene un [registro de MCP](https://github.com/mcp) para descubrir servidores.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Revisa su código fuente, confirma quién los publica y valora las implicaciones de seguridad antes de conceder acceso a recursos sensibles.

## Revisa la configuración MCP

`.vscode/mcp.json` configura los servidores del espacio de trabajo.

1. Abre `.vscode/mcp.json` y comprueba que incluye el servidor remoto `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

La plantilla del proyecto ya incluye la entrada `github`, que permitió a Copilot consultar el backlog en el ejercicio anterior. Se conecta por HTTP al servidor GitHub MCP remoto y se autentica con GitHub la primera vez que Copilot utiliza una de sus herramientas.

## Añade el servidor Playwright MCP

El servidor local Playwright MCP proporciona a Copilot un navegador controlable para probar la funcionalidad.

1. Añade la entrada local `playwright` junto a `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

La opción `--headless` ejecuta el navegador sin una ventana visible, necesaria en un codespace sin escritorio.

## Inicia y confía en el servidor

VS Code inicia los servidores MCP cuando Copilot necesita sus herramientas y pide confirmar que confías en ellos.

1. Si aparece **Start** sobre la entrada de Playwright en `.vscode/mcp.json`, selecciónalo.
2. Si VS Code te pide confirmar que confías en el servidor, revisa la configuración y acepta solo si confías en ella.

Iniciarlo manualmente es opcional. Si omites este paso, VS Code lo iniciará y pedirá que confirmes que confías en él cuando Copilot necesite sus herramientas.

## Prueba los filtros

El servidor Playwright MCP utiliza el árbol de accesibilidad de la página, por lo que la comprobación funcional también permite detectar problemas básicos de accesibilidad.

1. Asegúrate de que el servidor del sitio está activo en `http://localhost:4321`.
2. En Copilot Chat, pide que compruebe los filtros:

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

3. Compara el informe con los criterios de aceptación de la incidencia y pide correcciones si algo no funciona.

> [!NOTE]
> La aplicación debe estar ejecutándose en `http://localhost:4321`. Si se ha detenido, vuelve a iniciarla. Si Copilot indica que falta un navegador, pídele que ejecute `npx playwright install chromium`.

## Publica la rama y crea una solicitud de incorporación de cambios

Publica primero la rama desde el panel de control de código fuente.

1. En VS Code, abre **Source Control** y revisa los cambios.

   ![Captura del panel Source Control con los cambios realizados por Copilot.](../../../_images/ex3-source-control-changes.png)
2. Selecciona **+** para prepararlos y utiliza **Sparkle** para generar un mensaje de commit.
3. Selecciona **Publish** para enviar la rama al repositorio.

## Crea la solicitud de incorporación de cambios

Copilot puede localizar la incidencia correspondiente y vincularla a la solicitud.

1. En Copilot Chat, selecciona **New Chat** y confirma que está seleccionado **Agent**.
2. Envía este prompt:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

3. Selecciona **Continue** cuando sea necesario permitir las operaciones. Si Copilot solicita autenticación con GitHub, sigue las instrucciones.
4. Abre el enlace a la solicitud de incorporación de cambios y revísala, pero no la combines todavía.

## Resumen y pasos siguientes

Has:

- aprendido qué es MCP y cómo amplía las herramientas de Copilot.
- añadido el servidor Playwright MCP al espacio de trabajo.
- pedido a Copilot que probara manualmente la funcionalidad de filtrado en un navegador.
- publicado la rama y abierto una solicitud de incorporación de cambios para el trabajo de filtrado.

Continúa y [crea un agente personalizado][next-lesson] para agilizar las revisiones de accesibilidad.

## Recursos

- [Acerca de MCP][mcp-blog-post]
- [Servidor Playwright MCP][playwright-mcp-server]
- [Servidor GitHub MCP][github-mcp-server]
- [Registro de servidores MCP][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
