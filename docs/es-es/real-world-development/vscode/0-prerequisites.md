---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios de VS Code, prepara el entorno. Crearás una copia propia del repositorio Tailspin Toys, iniciarás un [codespace][codespaces] y comprobarás que GitHub Copilot Chat funciona en el editor.

## Configura el repositorio del taller

Crearás una copia del repositorio a partir de la [plantilla][template-repository].

1. En una ventana nueva del navegador, abre la [plantilla de Tailspin Toys][tailspin-template].
2. Selecciona **Use this template** y, después, **Create a new repository**.

   ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si participas en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. De lo contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.

   ![Configuración de la plantilla del repositorio](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio (`organization-or-user-name/repository-name`), porque la necesitarás más adelante.

> [!NOTE]
> **El backlog está preparado**
>
> Al crear el repositorio desde la plantilla, se genera automáticamente un backlog de incidencias de GitHub. Trabajarás con esas incidencias durante el taller; no tienes que crearlas.

## Crea un codespace

Utilizarás un codespace para completar los ejercicios. [GitHub Codespaces][codespaces] es un entorno de desarrollo en la nube que permite escribir, ejecutar y depurar código en el navegador.

1. Ve al repositorio que acabas de crear.
2. Selecciona **Code**.

   ![Botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, **+** para crear un codespace.

   ![Crear un codespace](../../../_images/ex0-create-codespace.png)

La creación puede tardar varios minutos. Deja el codespace abierto en una pestaña; volverás a él en un ejercicio posterior.

> [!CAUTION]
> Este taller también se puede ejecutar en un [contenedor de desarrollo][dev-containers] local. Abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te solicite.

## Usa GitHub Copilot Chat y el modo de agente

La extensión GitHub Copilot Chat debería estar instalada en el IDE si utilizas un codespace.

> [!TIP]
> Si falta, [instálala desde Visual Studio Code Marketplace][copilot-chat-extension] o abre la vista Extensions de Visual Studio Code, busca **GitHub Copilot Chat** y selecciona **Install**.

1. Vuelve al codespace.
2. Si Copilot Chat no aparece a la derecha del editor, selecciona su icono en la parte superior del codespace.
3. Escribe `Hello world` en Copilot Chat y pulsa <kbd>Enter</kbd>.
4. Si se te solicita, inicia sesión en GitHub siguiendo las instrucciones.

   ![Ejemplo del mensaje de autenticación de Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Comprueba que aparece la ventana de Copilot Chat.

## Resumen

Has creado una copia del repositorio del taller y has iniciado la configuración de un codespace para escribir código.

## Siguiente paso

Continúa con el [ejercicio 1: Instrucciones personalizadas][next-lesson], donde enseñarás a Copilot las convenciones del proyecto.

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Introducción a Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
