---
title: "Lección 5: Personalizar y utilizar la habilidad quality-checks"
description: "Explora la habilidad quality-checks, adapta el formato del informe y utilízala para comprobar los filtros."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Programar no consiste solo en escribir código. Ya has comprobado manualmente el funcionamiento y utilizado archivos de instrucciones para seguir los estándares. También hay que ejecutar pruebas, lint y otras comprobaciones de integración continua (CI).

Las **habilidades de agente** son adecuadas para estas tareas. Ayudan a Copilot a entender cómo realizar operaciones repetibles.

En esta lección:

- explorarás la habilidad existente `quality-checks`.
- personalizarás el formato de los resultados.
- volverás a cargar la habilidad y la ejecutarás.

## Escenario

Tailspin Toys utiliza `quality-checks` para pruebas unitarias, lint y comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las habilidades de agente agrupan instrucciones de tareas reutilizables, scripts ejecutables y recursos auxiliares que el agente carga cuando los necesita. Una habilidad se guarda en una carpeta con un archivo Markdown `SKILL.md`. El archivo contiene metadatos con el nombre y la descripción, una explicación de la habilidad y directrices sobre cuándo utilizarla. La carpeta también puede incluir scripts y otros recursos.

> [!NOTE]
> Una habilidad no necesita archivos ni carpetas adicionales. La habilidad `quality-checks` de Tailspin Toys solo contiene `SKILL.md`, porque utiliza los comandos existentes del proyecto.

Las habilidades pueden estar en `.github/skills` para compartirlas en el repositorio, o en la carpeta de habilidades del usuario, normalmente `~/.copilot/skills`.

## Explora la habilidad

Revisa la habilidad existente para entender qué instrucciones recibe Copilot antes de personalizarla.

1. Vuelve al codespace y abre `.github/skills/quality-checks/SKILL.md` en el editor.
2. Lee el `name` y la `description` de la parte superior. La descripción ayuda a Copilot a decidir cuándo utilizar la habilidad.
3. Lee las instrucciones y observa cómo orientan las pruebas y lint.
4. Comprueba que aún no hay una sección **Results output formatting**.

## Ejecuta la habilidad antes de cambiarla

Ejecuta la habilidad una vez con sus instrucciones actuales para tener un resultado de referencia.

1. Vuelve a la conversación de filtrado en modo Interactive.
2. Envía este prompt:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Revisa el informe.

## Personaliza el informe

Añadirás instrucciones para indicar qué se ejecutó y qué resultado obtuvo cada herramienta.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade al final del archivo esta sección:

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la habilidad actualizada

Copilot CLI puede volver a cargar las habilidades editadas sin reiniciar la conversación.

Vuelve a cargar la habilidad y repite la comprobación para revisar el nuevo formato del informe.

1. Ejecuta:

   ```plaintext
   /skills reload
   ```

2. Envía el mismo prompt:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Revisa el informe y compáralo con el primero.

## Resumen y pasos siguientes

Has:

- explorado la habilidad `quality-checks`.
- personalizado el formato de los resultados.
- vuelto a cargar y ejecutar la habilidad.

A continuación, permitirás que Copilot interactúe directamente con el sitio [mediante el servidor Playwright MCP][next-lesson].

## Más ejemplos de habilidades

Estos ejemplos de la comunidad sirven de referencia, no son tareas adicionales. Antes de adoptarlos, revisa sus requisitos y comportamiento:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de contribuciones: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y script de exportación: `drawio`][drawio-example]
- [Pruebas de navegador: `webapp-testing`][browser-example]

El ejemplo de contribuciones ascendente se llama `make-repo-contribution`; algunas plantillas antiguas de Tailspin utilizaban `make-contribution`. Este taller no depende de ninguna de las dos habilidades.

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
