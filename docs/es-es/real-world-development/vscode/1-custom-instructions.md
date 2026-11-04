---
title: "Ejercicio 1: Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El contexto es fundamental al trabajar con IA generativa. Los archivos de instrucciones explican a Copilot cómo debe estructurarse el código. En este ejercicio revisarás las instrucciones del proyecto, generarás una función auxiliar de editoriales con las instrucciones actuales y, después, añadirás un estándar de documentación para comparar el resultado.

En este ejercicio:

- revisarás el contexto del proyecto, las convenciones y la documentación mediante archivos de instrucciones generales y específicos de rutas.
- generarás el primer componente de datos para los filtros.
- añadirás un estándar general a `.github/copilot-instructions.md` y repetirás el prompt.
- confirmarás los cambios en `main` para que se utilicen en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede no seguir todos los estándares: Copilot no es determinista. El objetivo es observar la tendencia tras cambiar las instrucciones, no obtener siempre el mismo código.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene estándares de desarrollo: las pruebas unitarias son obligatorias para la capa de datos; la interfaz debe tener un tema oscuro moderno; el código debe incluir comentarios TSDoc; y cada archivo debe empezar con un bloque de comentarios que explique su propósito.

### Instrucciones personalizadas

`.github/copilot-instructions.md` se aplica a todas las solicitudes del repositorio. Los archivos `.github/instructions/*.instructions.md` pueden definir instrucciones para tipos de archivos o tareas concretos. En el IDE, se usan para generar código en Copilot Chat, pero no para completados de código ni sugerencias de siguiente edición. Copilot Chat, Copilot CLI y el agente en la nube también utilizan instrucciones con `applyTo`. Copilot admite otros estándares, como AGENTS.md y CLAUDE.md.

### Buenas prácticas para gestionar los archivos de instrucciones

Mantén el archivo general centrado en el proyecto y sus estándares. Usa archivos `*.instructions.md` para ámbitos concretos y escribe las directrices en lenguaje claro, con ejemplos. No existe una única forma correcta de organizar las instrucciones; experimenta con la que funcione para el proyecto.

> [!TIP]
> Explora las instrucciones del proyecto para [interfaz de usuario][ui-instructions] y [Astro][astro-instructions], y consulta [Awesome Copilot][awesome-copilot] para ver ejemplos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora las instrucciones del proyecto

1. Abre `.github/copilot-instructions.md` y revisa la descripción del proyecto, **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**, incluida la guía de **GitHub Actions Workflows**.
2. Explora `.github/instructions`, donde encontrarás directrices para Astro, Drizzle, pruebas y otros ámbitos.
3. Abre `.github/instructions/unit-tests.instructions.md` y comprueba el campo `applyTo`. Por ejemplo, coincide con archivos TypeScript como `**/*.test.ts`.
4. Revisa las instrucciones específicas para las pruebas unitarias.
5. Abre `.github/instructions/drizzle.instructions.md` y examina sus enlaces a otras instrucciones y archivos. Las rutas son relativas al propio archivo de instrucciones.

> [!NOTE]
> **Code formatting requirements** documenta los estándares existentes, pero aún no exige documentación en el código. Añadirás comentarios TSDoc y encabezados de archivo.

## Crea una rama

Trabaja en una rama propia para mantener separados estos cambios.

1. Vuelve al codespace y abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Crea y selecciona una rama:

   ```bash
   git checkout -b custom-instructions
   ```

## Usa Copilot Chat antes de cambiar las instrucciones

Inicia un chat nuevo para comparar el mismo prompt antes y después de actualizar las instrucciones.

1. Cierra las pestañas abiertas de ejercicios anteriores.
2. Abre `src/lib/publishers.ts` para indicar dónde debe ubicarse la función auxiliar.
3. En el selector de agentes de Chat, selecciona **Agent**.

   ![Captura del selector de agentes en la vista Chat, con Agent seleccionado.](../../../_images/shared-chat-mode-selector.png)
4. Envía este prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Revisa la función auxiliar tipada y las pruebas que Copilot haya creado. Observa que la función recibe primero el cliente `db` y devuelve una matriz tipada de editoriales, según las convenciones de acceso a datos de `.github/instructions/drizzle.instructions.md`. Comprueba si faltan los comentarios TSDoc y el encabezado del archivo.

> [!CAUTION]
> Copilot puede añadir comentarios aunque no se lo pidas. El objetivo es observar si las instrucciones mejoran la coherencia.

## Añade un estándar para todo el repositorio

Ahora añade a las instrucciones generales los estándares de documentación que compararás en el siguiente paso.

1. Abre `.github/copilot-instructions.md` y localiza **Code formatting requirements**, aproximadamente en la línea 27.
2. Añade estas líneas después de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

3. Guarda el archivo.

## Repite el prompt y observa el cambio

Vuelve a enviar el mismo prompt en un chat nuevo para comprobar si Copilot aplica el estándar que acabas de añadir.

1. En Copilot Chat, selecciona **New Chat** y vuelve a abrir `src/lib/publishers.ts`.
2. Envía exactamente el mismo prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

3. Comprueba si el archivo incluye un comentario inicial sobre su propósito y la función exportada incluye un comentario TSDoc con su propósito, parámetros y valor devuelto.

El encabezado debería ser similar a este:

```typescript
/**
 * Funciones auxiliares de acceso a datos de editoriales para la plataforma de
 * financiación colectiva de Tailspin Toys. Recupera información de editoriales
 * de la base de datos.
 */
```

El comentario de la función debería ser similar a este:

```typescript
/**
 * Devuelve una lista de todas las editoriales con su id y su nombre.
 *
 * @param db - Cliente de base de datos de Drizzle.
 * @returns Promesa que se resuelve en un array de objetos de editoriales.
 */
```

## Confirma y publica la rama

Revisa y publica los cambios de instrucciones y de la función auxiliar para que el equipo pueda utilizarlos.

1. Abre un terminal con <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) y comprueba los cambios:

   ```bash
   git status
   ```

2. Añade el archivo de instrucciones, la función auxiliar y cualquier prueba o archivo de apoyo que haya cambiado; después, crea el commit:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra otros archivos modificados, añádelos también.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

3. Publica la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Pide a Copilot que vincule la actualización con la incidencia correspondiente y combine la solicitud después de revisar las operaciones que propone.

1. Abre Copilot Chat y selecciona **Agent**.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir Copilot Chat y confirma que está seleccionado **Agent**.
3. Envía este prompt:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Revisa las operaciones de GitHub que Copilot solicite y selecciona **Allow** solo si apruebas cada acción.
5. Cuando se cree la solicitud, envía este prompt para pedir que la combine en `main` y actualice la rama local:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

6. Revisa las operaciones de GitHub y del terminal antes de permitirlas.

Has combinado una solicitud de incorporación de cambios con ayuda de Copilot.

## Resumen y pasos siguientes

Has:

- explorado cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- generado la función auxiliar de editoriales con las instrucciones existentes.
- añadido un estándar general a `.github/copilot-instructions.md`.
- observado el efecto de las instrucciones en el código generado.
- confirmado los cambios para que el siguiente ejercicio pueda utilizarlos.

Continúa y [utiliza el modo de agente][next-lesson] para añadir una funcionalidad en varias partes del proyecto.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
