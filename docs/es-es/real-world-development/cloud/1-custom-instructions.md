---
title: "Ejercicio 1: Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

El contexto es fundamental al trabajar con IA generativa. Los archivos de instrucciones explican a Copilot no solo qué debe hacer, sino cómo hacerlo. En este ejercicio revisarás las instrucciones del repositorio y añadirás un estándar general para que el agente en la nube lo aplique en las tareas posteriores.

En este ejercicio:

- revisarás cómo las instrucciones del repositorio y las instrucciones específicas de rutas proporcionan contexto a Copilot.
- añadirás un estándar general al repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los entornos de VS Code y CLI, aquí no compararás prompts antes y después. El agente en la nube trabaja de forma asíncrona con incidencias de GitHub, por lo que es más difícil mostrar el efecto en tiempo real. Verás cómo influyen las instrucciones cuando revises las solicitudes de incorporación de cambios que genere.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices de desarrollo. La capa de datos necesita pruebas unitarias, la interfaz debe tener un tema oscuro moderno, el código debe incluir comentarios TSDoc y cada archivo debe empezar con un bloque de comentarios que explique su propósito.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias, como convenciones de código, bibliotecas y comentarios. Se pueden definir para todo el repositorio o para tipos de archivos y tareas concretos.

- `.github/copilot-instructions.md` se envía a Copilot en todas las solicitudes del repositorio y debe contener información general del proyecto.
- `.github/instructions/*.instructions.md` puede incluir directrices para lenguajes, tipos de archivos o tareas específicos.

> [!NOTE]
> En un IDE, los archivos de instrucciones se utilizan para generar código en Copilot Chat, no para completar código ni para las sugerencias de siguiente edición. Copilot Chat, Copilot CLI y el agente en la nube también utilizan instrucciones del repositorio y archivos `*.instructions.md` con metadatos `applyTo`. Copilot admite otros formatos, como AGENTS.md y CLAUDE.md.

### Buenas prácticas para gestionar los archivos de instrucciones

Conviene mantener las instrucciones generales centradas en el proyecto y sus estándares, y usar archivos `*.instructions.md` para tipos de archivos o tareas concretas. Escríbelas en lenguaje claro e incluye ejemplos. No hay una única forma correcta de organizar las instrucciones: ajústalas a tu proyecto.

> [!TIP]
> Los archivos de instrucciones pueden enlazar otras instrucciones y ejemplos del proyecto. Consulta las instrucciones de [interfaz de usuario][ui-instructions] y [Astro][astro-instructions], o busca plantillas en [Awesome Copilot][awesome-copilot].

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones del proyecto

Revisa los archivos que incluye el repositorio en la interfaz web de GitHub o en un codespace:

1. Abre `.github/copilot-instructions.md` y revisa la descripción del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**, incluida la guía de **GitHub Actions Workflows**.
2. Explora `.github/instructions` y sus instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros ámbitos.
3. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`, que define el patrón relativo a la raíz del repositorio. Por ejemplo, coincide con archivos de pruebas TypeScript como `**/*.test.ts`.
4. Revisa las instrucciones para crear pruebas unitarias.
5. Abre `.github/instructions/drizzle.instructions.md` y observa los enlaces a otras instrucciones y archivos del proyecto. Las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> La sección **Code formatting requirements** establece los estándares del proyecto, pero aún no exige documentación dentro del código. Añadirás las reglas para TSDoc y los encabezados de archivo.

## Añade un estándar para todo el repositorio

Añade el estándar para que el agente en la nube lo lea cuando trabaje en incidencias dirigidas a `main`.

1. En un terminal del codespace, crea una rama:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Abre `.github/copilot-instructions.md` y localiza **Code formatting requirements**, aproximadamente en la línea 27.
3. Añade estas líneas después de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

El archivo general del repositorio es el lugar adecuado para estos estándares, porque se aplican al proyecto completo.

## Confirma y combina la actualización

El agente en la nube lee instrucciones de la rama a la que se dirige la incidencia. Debes combinar los cambios en `main` para que los utilice en el siguiente ejercicio.

1. Prepara y confirma el archivo:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Publica la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una solicitud de incorporación de cambios de `custom-instructions-cloud` a `main` y combínala. Si prefieres usar `main` directamente en este taller, puedes omitir la rama y confirmar los cambios directamente en `main`.

## Resumen y pasos siguientes

Has:

- explorado cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- añadido un estándar general a `.github/copilot-instructions.md`.

Verás el efecto de las instrucciones en las solicitudes de incorporación de cambios que genere el agente en la nube.

Continúa y [asigna tu primera incidencia al agente de GitHub Copilot en la nube][next-lesson].

## Recursos

- [Instrucciones para personalizar GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
