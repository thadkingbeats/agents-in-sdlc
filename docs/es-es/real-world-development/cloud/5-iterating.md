---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de que el equipo revise los cambios, comprobarás cómo se desarrollaron y pedirás ajustes al agente si es necesario.

## Revisa el trabajo

### Escenario

Durante este taller has trabajado con Copilot en tareas de documentación, una funcionalidad de juegos relacionados y mejoras de accesibilidad con modos de alto contraste y claro. Revisa los cambios y, si hace falta, pide al agente que los corrija antes de que el equipo los incorpore. El diseño de software y DevOps siguen requiriendo revisión aunque se utilice IA generativa.

## Seguridad del agente en la nube

El agente trabaja de forma asíncrona con medidas de seguridad:

- Solo tiene acceso de lectura al repositorio y acceso de escritura a su propia rama.
- Trabaja dentro de GitHub Actions, en un entorno efímero independiente para la tarea.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de ejecutarlos.
- El acceso a recursos externos, incluidos los servidores que utilizan el protocolo de contexto del modelo (MCP), está limitado de forma predeterminada. Puedes [configurar el firewall del agente][agent-firewall].

## Revisa la documentación generada

Empieza por la solicitud de incorporación de cambios que documenta el código y comprueba tanto los cambios como las comprobaciones.

1. En el repositorio de github.com, selecciona **Pull Requests** y abre la solicitud titulada, por ejemplo, **Add missing documentation**.
2. Si todavía aparece la marca **[WIP]**, espera a que Copilot termine.
3. Selecciona **Files changed** y revisa los cambios.
4. Comprueba los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentarios que proceden de las instrucciones del repositorio.
5. Vuelve a **Conversation**. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows** y espera a que pasen las comprobaciones del proyecto.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

   ![Acción Approve and run workflows para aprobar los flujos de trabajo pendientes.](../../../_images/shared-approve-workflows.png)

> [!NOTE]
> Es normal que la solicitud muestre una advertencia de que el firewall bloqueó a Copilot. De forma predeterminada, el agente tiene acceso limitado a recursos externos, incluidas las llamadas a servidores MCP.

## Pide cambios a Copilot

Puedes mencionar a Copilot en un comentario de la solicitud o en un comentario de código para iniciar otra sesión. Por ejemplo, puedes pedir encabezados de comentario para los archivos, comentarios TSDoc para TypeScript y Astro, o un README que describa la estructura de la aplicación Astro.

1. Añade un comentario a la solicitud y menciona a **@copilot** con la actualización que quieras.
2. Selecciona **View Session** para seguir el trabajo de Copilot. Puedes volver a la solicitud con **Back to pull request**.
3. Cuando Copilot termine, revisa el nuevo commit en **Files changed**.
4. Itera hasta que el resultado sea adecuado. Después, marca la PR como lista para revisión y combínala.

![Botón Back to pull request](../../../_images/ex7-back-to-pr.png)

![Acción para marcar la solicitud de incorporación de cambios como lista para revisión.](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

La siguiente PR contiene los cambios de la funcionalidad solicitada por el equipo de diseño.

1. En **Pull Requests**, abre la PR titulada, por ejemplo, **Show related games on the game details page**.
2. Revisa el código en **Files changed**.
3. En **Conversation**, selecciona **Approve and run workflows** si hay flujos de trabajo pendientes y espera a que pasen las comprobaciones.

   ![Acción Approve and run workflows para aprobar los flujos de trabajo pendientes.](../../../_images/shared-approve-workflows.png)
4. Opcionalmente, cambia a la rama del agente en tu codespace para probar la funcionalidad. Sustituye `<branch-name>` por el nombre de la rama:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Puedes solicitar otros cambios con un comentario en **Conversation**. Por ejemplo, ajustar el número de juegos relacionados o añadir encabezados y comentarios TSDoc.

## Revisa las mejoras de accesibilidad

La PR debe incluir el modo de alto contraste asignado en el ejercicio 3 y el modo claro solicitado en el ejercicio 4.

1. En **Pull Requests**, abre la solicitud titulada, por ejemplo, **Add high contrast mode to website**. Si sigue marcada como **[WIP]**, espera a que termine el agente.
2. En **Files changed**, revisa los controles de los modos, el almacenamiento local de preferencias, los estilos, los atributos de accesibilidad y el código que gestiona los modos.
3. En **Conversation**, selecciona **Approve and run workflows** si corresponde y espera a que pasen las comprobaciones.

   ![Acción Approve and run workflows para aprobar los flujos de trabajo pendientes.](../../../_images/shared-approve-workflows.png)
4. Opcionalmente, cambia a la rama del agente en el codespace y prueba que ambos modos funcionan y se conservan al recargar la página:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Si encuentras problemas de accesibilidad, menciona a **@copilot** en un comentario y solicita cambios.

Copilot incorporará la nueva solicitud al flujo de trabajo después de terminar el paso que estaba ejecutando cuando enviaste el mensaje. La tarea puede tardar varios minutos; mientras tanto, puedes repasar lo que has aprendido.

## Ejercicio opcional: sigue delegando

Crea más incidencias y asígnalas al agente en la nube para practicar. Por ejemplo, añade un formulario de interés para patrocinadores, implementa paginación en la lista de juegos o valida las entradas y gestiona errores en las funciones auxiliares de acceso a datos.

## Resumen

Has revisado las instrucciones personalizadas, asignado incidencias al agente en la nube, utilizado un agente de accesibilidad, supervisado y orientado la sesión desde la página de agentes, y revisado e iterado sobre sus solicitudes de incorporación de cambios.

## Repaso y pasos siguientes

Has terminado el entorno del agente en la nube. Puedes continuar con otros entornos:

- [Entorno de VS Code](../../vscode/): utiliza Copilot Chat en modo de agente e integración MCP desde el IDE.
- [Entorno de CLI](../../cli/): entrega cambios desde el terminal con Plan, Autopilot, habilidades, agentes personalizados, Playwright MCP y Agent Merge.

También puedes asignar incidencias de refactorización o cobertura de pruebas, crear agentes especializados o configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el firewall del agente en la nube][agent-firewall]

[previous-lesson]: ../4-managing-agents/
[github-copilot]: https://github.com/features/copilot
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
