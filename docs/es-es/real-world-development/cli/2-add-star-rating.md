---
title: "Lección 2: Añadir valoraciones con estrellas, una mejora rápida"
description: "Haz un cambio pequeño en las tarjetas de juegos con Copilot CLI, pruébalo en el navegador reenviado y combina tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ya has instalado Copilot CLI y probado una conversación. Ahora realizarás un cambio pequeño: los juegos ya tienen una valoración con estrellas en sus datos, pero las tarjetas de la página de inicio no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo combinarás en tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una conversación de Copilot en una rama de funcionalidad.
- pedirás al agente un cambio pequeño en el proyecto.
- revisarás el cambio con `/diff`.
- ejecutarás la aplicación y comprobarás el cambio en el navegador reenviado.
- abrirás y combinarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración con estrellas, que ya aparece en la página de detalles. Las tarjetas de la página de inicio solo muestran el título, la categoría, la editorial y la descripción. Como ejercicio inicial, pedirás que se muestre la valoración existente en cada tarjeta.

## Conversaciones en Copilot CLI

Una conversación es una sesión de trabajo con Copilot CLI. A diferencia de la aplicación Copilot, una conversación normal de CLI utiliza el repositorio y la rama activos en el terminal, en vez de crear automáticamente un árbol de trabajo. Las conversaciones guardadas permiten volver al mismo intercambio; los archivos y la rama siguen siendo el estado normal de Git en el disco.

En la conversación verás tus prompts y las respuestas del agente, su actividad con herramientas y los cambios que puedes revisar con `/diff`.

## Inicia una conversación y solicita el cambio

1. Vuelve al codespace.
2. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Si Copilot CLI no está en ejecución, inicia la herramienta:

   ```bash
   copilot --yolo
   ```

4. Ejecuta `/new` y pulsa <kbd>Enter</kbd> para iniciar una sesión nueva.
5. Envía este prompt:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot explorará el proyecto, localizará los archivos de las tarjetas de juego y realizará los cambios.

## Revisa las diferencias

1. Ejecuta `/diff` y revisa todos los archivos modificados.
2. Confirma que las tarjetas muestran la valoración numérica cuando existe y `No rating yet` cuando `starRating` es `null`.
3. Confirma que las pruebas cubren ambos casos y revisa los resultados de las comprobaciones.
4. Pide al agente que corrija los fallos y vuelve a comprobarlos.
5. Cuando termines, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.

> [!NOTE]
> Copilot es probabilístico, por lo que el código exacto puede variar. Comprueba el comportamiento, no una implementación concreta.

## Comprueba el cambio

1. Pide a Copilot que inicie el sitio para inspeccionar el cambio en el navegador reenviado por Codespaces:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Confirma que las tarjetas muestran las valoraciones sobre cinco.
4. Vuelve a Copilot y pídele que detenga el servidor que inició:

   ```plaintext
   Stop the development server you started.
   ```

## Abre y combina tu primera solicitud de incorporación de cambios

1. Pide al agente predeterminado que confirme los cambios revisados:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Ejecuta `/pr create`. Copilot CLI enviará el commit existente y mostrará la URL de la solicitud.
3. Abre el enlace con <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) mientras lo seleccionas.
4. Revisa los archivos modificados y las comprobaciones.
5. Cuando todo esté listo, selecciona **Merge pull request** y confirma la combinación.
6. Vuelve al codespace y sal de Copilot CLI con `/exit`.
7. Actualiza la rama local `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumen y pasos siguientes

Has:

- iniciado una conversación de Copilot en una rama de funcionalidad.
- pedido al agente un cambio pequeño en el proyecto.
- revisado el cambio con `/diff`.
- ejecutado la aplicación y comprobado el cambio en el navegador reenviado.
- abierto y combinado tu primera solicitud de incorporación de cambios.

Continúa y [utiliza los modos Plan y Autopilot][next-lesson] para implementar una funcionalidad mayor.

## Recursos

- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
