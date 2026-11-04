---
title: "Lección 7: Crear y utilizar un agente de QA"
description: "Crea un agente de control de calidad que combine los requisitos de la incidencia, la habilidad quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has utilizado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y Playwright MCP para observar los filtros en un navegador. Ahora reunirás esas capacidades en un agente personalizado con un proceso de control de calidad (QA) definido.

En esta lección:

- explorarás cómo un agente personalizado utiliza instrucciones, habilidades y herramientas MCP.
- crearás y revisarás un perfil reutilizable de QA.
- seleccionarás el agente y revisarás sus conclusiones respecto a la incidencia de filtrado.

## Escenario

Antes de abrir una solicitud de incorporación de cambios (PR), Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador. Un agente personalizado puede coordinar el proceso y generar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una variante especializada de Copilot definida en un perfil Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles. En este taller, crearás el rol de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Cada personalización cumple una función distinta: las instrucciones del repositorio describen los estándares del equipo; la habilidad `quality-checks` agrupa comprobaciones repetibles; Playwright MCP proporciona herramientas de navegador; y el perfil de QA indica cómo evaluar los requisitos y presentar los resultados.

## Crea el perfil de QA

Antes de abrir la PR, pide a Copilot que cree un perfil reutilizable y defina sus responsabilidades y límites.

1. Vuelve al codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el perfil:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Revisa el perfil

1. Ejecuta `/diff` y abre `.github/agents/qa.agent.md`.
2. Comprueba que los metadatos incluyen `description`. `name` es opcional, pero ayuda a identificar el agente.
3. Confirma que las instrucciones empiezan por los requisitos, siguen las instrucciones del repositorio, ejecutan `quality-checks` y utilizan Playwright MCP.
4. Comprueba que el informe incluye pruebas que justifican los resultados, que el agente debe pedir permiso antes de modificar la implementación y que no puede confirmar cambios ni abrir PR.
5. Si falta alguna responsabilidad o límite, pide al agente predeterminado que revise el perfil.

## Ejecuta QA con la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Reanuda la conversación de filtrado después de crear el perfil y selecciona QA para que tenga acceso a la incidencia y las decisiones de planificación.

1. Sal de la conversación con `/exit` y reanúdala desde la raíz del repositorio:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado.
2. Para activar el agente, ejecuta:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, puede que no aparezca en la lista. El comando anterior lo activa.

3. Pide al agente que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

4. Confirma que utiliza la incidencia y las decisiones del plan correctas. Proporciona la URL de la incidencia o el contexto que falte.
5. Revisa el informe cuando termine.

## Resumen y pasos siguientes

Has:

- explorado cómo un agente personalizado utiliza instrucciones, habilidades y herramientas MCP.
- creado y revisado un perfil reutilizable de QA.
- seleccionado el agente y revisado sus conclusiones respecto a la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y las pruebas de verificación preparados. A continuación, [revisarás y combinarás la PR de funcionalidad con Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
