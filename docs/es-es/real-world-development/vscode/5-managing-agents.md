---
title: "Ejercicio 5: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En modo de agente, GitHub Copilot explora el código, propone cambios, edita archivos y ejecuta comandos. Copilot Chat en VS Code muestra las operaciones y los cambios mientras ocurren. Puedes revisar cada diferencia, aceptar o rechazar cambios y orientar la conversación con prompts de seguimiento.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos.
- pedirás al agente que añada un modo claro a la vez que el modo de alto contraste.

## Escenario

Mientras el agente implementa el modo de alto contraste, el equipo solicita también un modo claro. Continúa en la misma sesión para que el agente conserve el contexto del trabajo.

## Supervisa el progreso de Copilot

1. Vuelve a Copilot Chat del ejercicio anterior.
2. Observa las llamadas a herramientas, los archivos que explora y los comandos que propone.
3. Para cada diferencia en línea, selecciona **Keep** para aceptar el cambio o **Undo** para revertirlo.
4. Abre **Files changed** para revisar el conjunto completo de archivos modificados.
5. Espera al mensaje final que resuma los cambios del modo de alto contraste.

> [!NOTE]
> Si una llamada a una herramienta solicita permiso, por ejemplo, para ejecutar un comando de terminal, el agente se detiene y muestra **Allow**. Aprueba solo los comandos que aceptes.

## Pide al agente que añada el modo claro

1. En la entrada de Copilot Chat, envía este prompt de seguimiento:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. Revisa cada cambio nuevo con **Keep** o **Undo**.
3. Si el agente sigue un enfoque que no quieres, deténlo con **Stop** y envía un prompt para aclararlo.

> [!TIP]
> Un prompt de seguimiento permite corregir el rumbo sin empezar de nuevo. Puedes pedir que simplifique el CSS, integre el control en el panel existente o añada atajos de teclado.

## Revisa los cambios

1. Abre **Source Control** en VS Code.
2. Revisa todos los archivos modificados y sus diferencias.
3. Comprueba los atributos de Accessible Rich Internet Applications (ARIA), la navegación con teclado, el HTML semántico y la persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara los cambios y crea un commit desde el panel **Source Control**. Los publicarás en el ejercicio siguiente.

## Resumen y pasos siguientes

Has:

- supervisado en tiempo real el trabajo del agente de accesibilidad.
- revisado y aceptado o rechazado los cambios propuestos.
- pedido al agente que añadiera un modo claro junto al modo de alto contraste.

En el [siguiente ejercicio][next-lesson], publicarás los cambios de accesibilidad en una solicitud de incorporación de cambios y revisarás el trabajo del agente.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo de agente][agent-mode]

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
