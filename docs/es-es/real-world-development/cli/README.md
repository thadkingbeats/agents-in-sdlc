---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Desarrolla, verifica y entrega dos cambios de Tailspin Toys mientras exploras los modos de Copilot CLI, las personalizaciones, las herramientas MCP y la automatización de solicitudes de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** incorpora GitHub Copilot al terminal como asistente de programación con agentes. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas desde la línea de comandos, para que puedas mantener el flujo sin cambiar a un editor gráfico.

El taller recorre un flujo de trabajo continuo con Tailspin Toys:

1. Prepara el proyecto en GitHub Codespaces, instala Copilot CLI y familiarízate con el entorno.
2. Añade valoraciones con estrellas, revisa el resultado en el navegador y combina manualmente tu primera solicitud de incorporación de cambios (PR).
3. Empieza por la incidencia de filtrado, define el enfoque en modo Plan, impleméntalo en modo Autopilot y revísalo en modo Interactive.
4. Actualiza las instrucciones del repositorio y aplícalas al filtrado.
5. Personaliza la habilidad existente `quality-checks` y utilízala para ejecutar las comprobaciones del proyecto.
6. Añade el servidor Playwright Model Context Protocol (MCP) y úsalo para examinar los filtros en un navegador.
7. Crea un agente personalizado de control de calidad (QA) para revisar requisitos, cobertura y pruebas de verificación.
8. Revisa el cambio completo de filtrado y usa Agent Merge para combinar la PR.
9. Explora comandos de barra para gestionar el contexto, los modelos, el uso compartido y la delegación opcional al agente en la nube.

Crearás dos PR: una para las valoraciones y otra para el filtrado, las instrucciones, la habilidad, el perfil de QA y las pruebas. El flujo de filtrado y calidad comparte una conversación y una rama.

## Lecciones

| Lección | Tema | Descripción |
| ------ | ----- | ----------- |
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y codespace |
| [1. Instalar Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI y familiarízate con el entorno |
| [2. Añadir valoraciones con estrellas][ex2] | Primer cambio | Muestra las valoraciones existentes y el estado sin valoración; después, combina la primera PR |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica desde la incidencia, implementa con Autopilot y revisa en Interactive |
| [4. Orientar a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones y aplícalas al filtrado |
| [5. Personalizar y utilizar una habilidad quality-checks][ex5] | Comprobaciones repetibles | Explora la habilidad existente, cambia el formato del informe y ejecútala |
| [6. Validar con Playwright MCP][ex6] | Observación en navegador | Configura MCP en la CLI e inspecciona el filtrado |
| [7. Crear y utilizar un agente de QA][ex7] | Requisitos y cobertura | Crea y selecciona un perfil especializado y reúne pruebas de verificación |
| [8. Crear y combinar la PR de funcionalidad][ex8] | Revisión y combinación | Revisa el cambio completo, crea la PR y usa Agent Merge |
| [9. Comandos avanzados de Copilot CLI][ex9] | Funciones de CLI | Explora contexto, modelos, uso compartido y delegación opcional al agente en la nube |
| [10. Repaso y pasos siguientes][ex10] | Resumen | Repasa el flujo, las personalizaciones reutilizables y otros recursos |
| [Opcional: Incorporar Foundry][foundry] | Agentes hospedados | Prepara un modelo, despliega un agente basado en el catálogo y conéctalo al sitio |

## Requisitos previos

Antes de participar en el taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Permiso para crear un repositorio y un codespace
- [ ] Conocimientos básicos del terminal o la línea de comandos

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis a través de [GitHub Education][student-plan]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que utiliza este taller.

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, comprueba que el administrador haya habilitado Copilot CLI.

## Primeros pasos

**[Empieza con los requisitos previos →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
