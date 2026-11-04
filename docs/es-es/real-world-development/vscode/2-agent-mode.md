---
title: "Ejercicio 2: Añadir funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso los cambios sencillos pueden afectar a varios archivos y requerir pruebas. El modo de agente de Copilot explora el proyecto, identifica los archivos relevantes, coordina los cambios, ejecuta tareas y puede corregir los errores que detecte. En este ejercicio lo utilizarás para añadir filtros por categoría y editorial.

> [!NOTE]
> El modo de agente trabaja en el IDE con ciclos rápidos de interacción. El agente en la nube trabaja de forma asíncrona con incidencias y solicitudes de incorporación de cambios.

En este ejercicio:

- explorarás cómo el modo de agente identifica archivos y coordina cambios.
- implementarás una funcionalidad en la interfaz y la capa de datos.
- revisarás el código y las pruebas antes de combinar los cambios.

## Escenario

El catálogo de Tailspin Toys crece y los usuarios necesitan filtrar los juegos por categoría y editorial. Ya has creado la función auxiliar de editoriales en el ejercicio anterior; ahora completarás la capa de datos, la interfaz y las pruebas.

## Ejecuta el sitio de Tailspin Toys

El sitio es una aplicación Astro que genera HTML estático. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM. No hay una API de backend independiente ni un framework de interfaz en el cliente. Las funciones auxiliares reutilizables están en `src/lib/` y la interactividad utiliza scripts Astro acotados con las API estándar del DOM.

### Inicia el sitio

1. Vuelve al codespace y confirma que estás en `main`.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

5. Abre `http://localhost:4321` en el navegador. En Codespaces, el enlace se redirige a la URL privada del puerto reenviado.

### Explora el sitio

1. Revisa la página de inicio y una página de detalles de un juego.

## Explora el backlog con Copilot

Antes de comenzar, vuelve a Copilot Chat, selecciona **New Chat** y, en el selector de agentes, elige **Agent**.

![Captura del selector de agentes de Copilot Chat con Agent seleccionado.](../../../_images/shared-chat-mode-selector.png)

1. Selecciona **Claude Sonnet 4.5** en la lista de modelos.
2. Envía este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

3. Selecciona **Continue** para permitir que se enumeren las incidencias y revisa la lista.

## Revisa las instrucciones

Antes de pedir cambios, consulta las directrices de interfaz para saber qué contexto recibirá Copilot.

1. Abre `.github/instructions/ui.instructions.md`.
2. Revisa la arquitectura, los principios de diseño, las pruebas, la accesibilidad y los enlaces a las instrucciones de Astro, Tailwind CSS y Drizzle.

## Implementa los filtros

Completar los filtros requiere lógica en la capa de datos, pruebas y cambios en la página de listado.

1. En Copilot Chat, selecciona **New Chat** o continúa la conversación actual.
2. Selecciona **Add Context**, **Instructions** y **ui**.

   ![Captura del selector de instrucciones con el archivo de instrucciones de interfaz seleccionado.](../../../_images/ex3-select-instructions-file.png)
3. Confirma que el modo **Agent** y el modelo **Claude Sonnet 4.5** siguen seleccionados.
4. Envía este prompt:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

5. Revisa los archivos, las pruebas y cualquier permiso que solicite Copilot. Deja que ejecute las pruebas cuando te lo pida y examina el código propuesto.

   ![Captura de Copilot explorando archivos del proyecto durante la implementación.](../../../_images/ex3-agent-mode-explores.png)

   ![Captura de Copilot Chat con la solicitud de permiso para ejecutar las pruebas.](../../../_images/ex3-agent-mode-run-tests.png)

   ![Captura de una sesión de Copilot Chat con los cambios propuestos.](../../../_images/ex3-agent-mode-proposed-changes.png)

6. Prueba los filtros en el sitio y selecciona **Keep** en Copilot Chat solo cuando hayas revisado y confirmado los cambios.

> [!CAUTION]
> Revisa siempre el código generado por Copilot u otras herramientas de IA antes de aceptarlo.

## Resumen y pasos siguientes

Has:

- observado cómo el modo de agente explora el proyecto, encuentra archivos relevantes y coordina cambios.
- implementado una funcionalidad en la interfaz y la capa de datos.
- revisado el código y las pruebas antes de incorporar los cambios.

A continuación, [probarás la funcionalidad con el servidor Playwright MCP][next-lesson] y abrirás una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar paginación

Pide a Copilot que añada paginación a la lista de juegos. Sigue las instrucciones existentes, decide si el usuario puede seleccionar el tamaño de página y aporta el contexto necesario. Itera sobre la propuesta hasta que la implementación cumpla tus requisitos.

## Recursos

- [Modos Ask, Edit y Agent de Copilot][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
