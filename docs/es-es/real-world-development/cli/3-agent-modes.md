---
title: "Lección 3: Modos de agente: Plan y Autopilot"
description: "Usa Plan para acordar un enfoque, Autopilot para crear los filtros desde una incidencia e Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ya has añadido un cambio pequeño al proyecto. Los cambios mayores necesitan un proceso más completo. En las siguientes lecciones utilizarás un flujo de desarrollo con agentes: partir de una incidencia, planificar, implementar, probar, revisar y combinar.

> [!NOTE]
> Utilizarás la misma conversación y rama durante el trabajo de filtrado. En otros proyectos quizá dividirías los cambios en ramas o PR diferentes; aquí se agrupan para centrar el taller en los conceptos principales.

En esta lección:

- iniciarás una conversación de Copilot desde una incidencia de GitHub.
- definirás los requisitos en modo Plan.
- implementarás la funcionalidad en modo Autopilot.
- revisarás el código.
- probarás manualmente la funcionalidad en el navegador reenviado.

En las lecciones siguientes actualizarás las instrucciones del repositorio, personalizarás la habilidad `quality-checks`, añadirás validación MCP, crearás un agente de QA y abrirás la PR.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar los juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero hay detalles —como cómo combinar categorías— que deben acordarse antes de programar. Utilizarás Plan para decidirlos y después autorizarás una implementación acotada con Autopilot.

## Flujo de trabajo de desarrollo

La incorporación de agentes de programación con IA no cambia las bases del desarrollo. Un flujo habitual consiste en:

1. Abrir una incidencia que describa el trabajo.
2. Planificar qué se debe crear.
3. Implementar y revisar el código.
4. Ejecutar las pruebas.
5. Validar manualmente la funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Combinar el código después de la revisión y de que se completen correctamente las comprobaciones de integración continua.

El flujo concreto depende del equipo y la organización, pero seguir este proceso ayuda a comprobar que el código generado cumple los requisitos y pasa por la misma revisión que el código escrito manualmente.

## Modos de conversación

El **modo de conversación** controla la autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo:

- **Interactive**: trabajas con el agente; propone cambios y espera indicaciones antes de seguir.
- **Plan**: el agente primero crea un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma, escribe código, ejecuta pruebas e itera hasta completar la tarea.

Empieza en Plan, revisa el plan y después utiliza Autopilot para implementarlo.

## Empieza por la incidencia

Prepara el codespace y la rama antes de comenzar el trabajo de filtrado.

1. Vuelve al codespace. Si está detenido, reinícialo.
2. Confirma que la PR de valoraciones con estrellas está combinada.
3. Si no hay un terminal abierto, pulsa <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para los filtros:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Usa las teclas de dirección para seleccionar **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al prompt y volver a la pestaña **Session**.

El prompt empezará con una referencia como `#7`. El signo `#` permite añadir una incidencia o PR de GitHub al contexto.

## Planifica los filtros

Planificar permite acordar el enfoque antes de delegar la implementación.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para seleccionar el modo Plan. Confirma que el indicador debajo del prompt muestra **Plan**.
2. Después de la referencia a la incidencia, escribe:

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. Responde a las preguntas de Copilot sobre el comportamiento de los filtros.
4. Cuando termine, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandir el plan y revísalo.
5. Pide que revise cualquier parte que no refleje tus decisiones.

## Aprueba Autopilot

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente de tu versión.
2. Confirma que el indicador debajo del prompt muestra **Autopilot**.
3. Observa cómo Copilot sigue el plan, genera el código y ejecuta las pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación inmediatamente, así que revisa el plan antes. Si Copilot informa de dependencias ausentes o conflictos de puerto, resuelve el problema antes de considerar completas las comprobaciones.

## Revisa y verifica la implementación

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Interactive y confirma que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Ejecuta `/diff` y revisa la implementación de filtros y las pruebas.
3. Compara los cambios con la incidencia y las decisiones de planificación.
4. Pulsa <kbd>Esc</kbd> para salir de las diferencias.
5. Revisa los resultados de las comprobaciones del proyecto y pide a Copilot que corrija los fallos.

## Explora la funcionalidad

1. Pide a Copilot que inicie el sitio:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros por categoría y editorial y las combinaciones acordadas en el plan.
4. Comprueba que el reinicio y el estado sin resultados coinciden con la incidencia y tus decisiones.
5. Pide a Copilot que detenga el servidor de desarrollo que inició.

## Resumen y pasos siguientes

Has:

- iniciado una conversación de Copilot desde una incidencia de GitHub.
- definido los requisitos en modo Plan.
- implementado la funcionalidad en modo Autopilot.
- revisado el código.
- probado manualmente la funcionalidad en el navegador reenviado.

Continúa y [usa instrucciones personalizadas][next-lesson] para comprobar cómo afectan al código generado.

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
