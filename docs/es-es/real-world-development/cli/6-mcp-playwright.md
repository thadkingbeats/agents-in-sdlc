---
title: "Lección 6: Validar la funcionalidad con Playwright MCP"
description: "Comprueba si Playwright MCP está disponible o configúralo en Copilot CLI y explora los filtros en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Además de escribir código, el desarrollo requiere trabajar con datos, servicios externos y automatizaciones. Los servidores Model Context Protocol (MCP) amplían Copilot CLI con herramientas y servicios adicionales.

En esta lección:

- aprenderás qué es MCP y cómo lo utiliza Copilot CLI.
- añadirás el servidor Playwright MCP si aún no está disponible.
- pedirás al agente que controle un navegador para comprobar los filtros.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero la validación de la interfaz requiere interactuar con ella. Playwright MCP permite a Copilot utilizar el sitio como lo haría una persona y comprobar el comportamiento de la funcionalidad.

## ¿Qué es Model Context Protocol?

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de IA se comuniquen con herramientas y servicios externos en tiempo real para consultar información y realizar acciones. Un servidor MCP actúa como puente entre el agente y esas herramientas.

- **[GitHub MCP Server][github-mcp]** proporciona acceso a API para gestionar repositorios de GitHub, incidencias y solicitudes de incorporación de cambios.
- **[Playwright MCP Server][playwright-mcp-server]** automatiza un navegador mediante Playwright.

GitHub mantiene un [registro de MCP][mcp-registry] para facilitar el descubrimiento y las contribuciones.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de utilizar uno, revisa su código fuente, confirma quién lo publica y valora las implicaciones de seguridad.

## Añade el servidor Playwright MCP

Si Playwright MCP ya está disponible en Copilot CLI, omite la configuración y continúa con la prueba.

1. Vuelve al codespace e inicia Copilot CLI.
2. Abre el cuadro para añadir un servidor MCP:

   ```plaintext
   /mcp add
   ```

3. En el campo del nombre, escribe `playwright` y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** con <kbd>Enter</kbd> y pulsa <kbd>Tab</kbd>.
5. En el cuadro **Command**, introduce:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Guarda la configuración con <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux).
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Ya has comprobado manualmente el funcionamiento de los filtros. Ahora pide a Copilot que los valide con Playwright MCP.

1. Envía este prompt:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

Copilot suele elegir las herramientas MCP adecuadas según el contexto. Si ya sabes qué servidor debe utilizar, indicarlo ayuda a orientar la tarea.

2. Observa los pasos que ejecuta en el navegador.
3. Lee el informe y comprueba que el comportamiento coincide con lo acordado.

Copilot iniciará el servidor, abrirá un navegador, interactuará con el sitio y detendrá el servidor que haya iniciado antes de presentar el informe.

## Resumen y pasos siguientes

Has:

- aprendido qué es Model Context Protocol (MCP) y cómo lo utiliza Copilot CLI.
- añadido el servidor Playwright MCP si aún no estaba disponible.
- pedido al agente que controle un navegador y explore la funcionalidad de filtrado.

Continúa y [crea un agente personalizado de QA][next-lesson] que combine la habilidad y las herramientas del navegador.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de ello?][mcp-blog-post]
- [Servidor Playwright MCP de Microsoft][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
