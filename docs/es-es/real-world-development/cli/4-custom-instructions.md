---
title: "Lección 4: Orientar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es fundamental al trabajar con IA generativa. Si una tarea debe realizarse de una forma concreta, proporciona a Copilot las instrucciones necesarias. Los archivos de instrucciones explican no solo qué código quieres, sino también cómo debe estructurarse. Ahora que has creado los filtros, revisarás las instrucciones utilizadas, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- explorarás cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- actualizarás las instrucciones para que se respeten los estándares de código.
- observarás su efecto en el código generado.

## Escenario

Tailspin Toys tiene estándares de desarrollo:

- Los comentarios deben explicar la intención y las decisiones que no sean obvias, no repetir el código.
- Las funciones exportadas de `db/` y `src/lib/` deben documentar su propósito, parámetros y valor devuelto con TSDoc/JSDoc, incluido el argumento `db` inyectable cuando corresponda.
- Los componentes Astro reutilizables deben documentar sus contratos `Props`, y los comentarios deben mantenerse actualizados cuando cambia el código relacionado.
- Se deben conservar las directrices de formato y lint existentes.

Los archivos de instrucciones permiten proporcionar a Copilot la información necesaria para seguir estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan contexto y preferencias para orientar las respuestas de Copilot. Puedes indicar convenciones de código, bibliotecas y comentarios, ya sea para todo el repositorio o para tipos de archivos y tareas específicos.

- `.github/copilot-instructions.md` se envía a Copilot en todas las solicitudes del repositorio. Debe contener información general del proyecto y directrices relevantes para la mayoría de las solicitudes.
- `.github/instructions/*.instructions.md` contiene directrices para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> La compatibilidad con otros formatos e instrucciones varía según el entorno. Consulta la [referencia de compatibilidad con instrucciones personalizadas][custom-instructions-support] antes de depender de un formato específico.

## Explora los archivos de instrucciones personalizados del proyecto

1. Vuelve al codespace y, en el editor, abre `.github/copilot-instructions.md`.
2. Revisa la descripción breve del proyecto y las directrices de código. Se aplican a todas las interacciones con Copilot en este repositorio.
3. Explora `.github/instructions`, donde hay instrucciones para Astro, la capa de datos Drizzle, pruebas y otros ámbitos.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa `applyTo`, que define el patrón de archivos al que se aplican las instrucciones.
5. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otras instrucciones y a archivos del proyecto.

## Actualiza las instrucciones del equipo

Añadirás comentarios TSDoc al código TypeScript nuevo.

1. En `.github/copilot-instructions.md`, localiza la sección **Code formatting guidance**, aproximadamente en la línea 35.
2. Añade este elemento al final de la sección:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guarda automáticamente.

## Aplica las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Cierra y reanuda la conversación de filtrado para que Copilot aplique la nueva directriz sin perder el contexto.

1. Si la conversación de filtrado sigue abierta, ejecuta `/exit`. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio, en la rama `game-filters-cli`, reanuda la conversación:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que está seleccionada la rama `game-filters-cli`.
3. Pide a Copilot que aplique las instrucciones actualizadas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Ejecuta `/diff` y revisa los archivos TypeScript modificados. Comprueba que los nuevos comentarios TSDoc describen el código correctamente.

## Resumen y pasos siguientes

Has:

- explorado cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- actualizado las instrucciones para que se respeten los estándares de código.
- observado su efecto en el código generado.

Continúa y [personaliza y ejecuta la habilidad reutilizable quality-checks][next-lesson] para ejecutar lint y pruebas de forma coherente.

## Recursos

- [Añadir instrucciones personalizadas a Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
