---
title: "Lección 1: Instalar GitHub Copilot CLI"
description: "Instala y autentica Copilot CLI en un codespace, explora el entorno y localiza la incidencia de filtrado del backlog."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] es un asistente de programación con agentes que se ejecuta en el terminal. Permite explorar bases de código, generar código, ejecutar comandos y utilizar herramientas externas desde la línea de comandos. En esta lección instalarás la herramienta, iniciarás sesión y la prepararás para el resto del taller.

En esta lección:

- instalarás GitHub Copilot CLI con npm.
- iniciarás sesión con tu cuenta de GitHub.
- confiarás en el repositorio del taller y probarás una conversación.
- localizarás la incidencia de filtrado mediante el servidor GitHub MCP integrado.

## Escenario

Tu equipo empieza a utilizar agentes de IA para abordar un backlog creciente. Copilot CLI lleva esta capacidad al terminal. Esta lección te permitirá instalarlo, autenticarte y prepararlo para el resto del taller.

## Instala Copilot CLI

Puedes instalar Copilot CLI con [npm][install-cli], WinGet o Homebrew. Como GitHub Codespaces incluye Node.js, utilizarás npm.

1. Vuelve al codespace y abre un terminal.
2. Comprueba que Node.js está instalado y cumple el requisito de versión:

   ```bash
   node --version
   ```

   Deberías ver la versión 24 o posterior.

3. Instala Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Comprueba la instalación:

   ```bash
   copilot --version
   ```

## Inicia sesión en GitHub

La primera vez que inicies Copilot CLI, se te pedirá que te autentiques con tu cuenta de GitHub.

1. Inicia Copilot CLI:

   ```bash
   copilot
   ```

2. Si se te solicita, sigue las instrucciones de autenticación con código de dispositivo.
3. Copilot CLI muestra este mensaje:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Comprueba que la ruta corresponde al repositorio de Tailspin Toys y selecciona **Yes, and remember this folder for future sessions**.

> [!NOTE]
> En un codespace, puede que ya hayas iniciado sesión mediante tu sesión de GitHub. Si Copilot CLI se inicia sin pedir autenticación, puedes continuar.

## Familiarízate con la CLI

Los comandos escritos en el prompt habitual se ejecutan directamente en el codespace. Una vez iniciado Copilot CLI, el lenguaje natural se envía al agente y los comandos de barra controlan la conversación.

1. Ejecuta `/model`, utiliza las teclas de dirección para seleccionar **Auto**, pulsa <kbd>Enter</kbd> y vuelve a pulsar <kbd>Enter</kbd> para confirmar.
2. Ejecuta `/help` para ver los comandos de la versión instalada y pulsa <kbd>Esc</kbd> para cerrar la ayuda.
3. Haz una pregunta sencilla para comprobar que funciona:

   ```plaintext
   What are the key files in this project?
   ```

4. Lee la respuesta y observa cómo Copilot explora el repositorio antes de responder.
5. Ejecuta `/mcp list` y confirma que está disponible el servidor GitHub MCP integrado.
6. Pide a Copilot que encuentre la incidencia de filtrado:

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. Abre la URL y lee la incidencia. La utilizarás después de un primer cambio rápido.

> [!TIP]
> Una sesión normal de Copilot CLI trabaja en la rama que esté seleccionada en el terminal; no crea automáticamente un árbol de trabajo. Crearás una rama de funcionalidad antes de cada cambio.

## Utiliza el atajo del taller

Normalmente Copilot CLI pide permiso antes de utilizar herramientas fuera de los permisos establecidos. En este taller volverás a iniciarlo con `--yolo`, un atajo aprobado por el usuario que elimina esas solicitudes dentro del codespace.

> [!CAUTION]
> `--yolo` habilita permisos automáticos completos (`--allow-all-tools`, `--allow-all-paths` y `--allow-all-urls`). Úsalo solo en un entorno aislado, como un codespace o una máquina virtual; no lo configures como opción predeterminada para el desarrollo diario. Consulta [Permitir y denegar el uso de herramientas][allow-all-warning].

En este taller, `--enable-all-github-mcp-tools` activa las herramientas GitHub MCP de lectura y escritura que utilizarás más adelante. El codespace limita el acceso a tu equipo, pero los recursos de GitHub a los que te autentiques son reales. Revisa los cambios antes de publicarlos o combinarlos.

1. Sal de Copilot CLI con `/exit`.
2. Vuelve a iniciarlo desde la raíz del repositorio:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Haz otra pregunta rápida sobre el proyecto y, después, sal con `/exit`.

Copilot guarda las conversaciones automáticamente. Más adelante, al modificar instrucciones o añadir un agente, utilizarás `copilot --resume` para volver a la conversación y la rama de filtrado.

## Resumen y pasos siguientes

Has:

- instalado GitHub Copilot CLI con npm.
- iniciado sesión con tu cuenta de GitHub.
- confiado en el repositorio del taller y probado una conversación.
- localizado la incidencia de filtrado mediante el servidor GitHub MCP integrado.

A continuación, [realizarás tu primer cambio acotado][next-lesson] y utilizarás Copilot CLI para mostrar las valoraciones de los juegos.

## Recursos

- [Instalar GitHub Copilot CLI][install-cli]
- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
