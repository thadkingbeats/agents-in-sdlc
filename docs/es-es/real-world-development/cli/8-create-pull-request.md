---
title: "Lección 8: Crear y combinar la PR de funcionalidad"
description: "Revisa los filtros, las instrucciones, la habilidad, el perfil de QA y las pruebas; después, crea la PR y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación de los filtros, las actualizaciones de instrucciones, la habilidad, el perfil de control de calidad (QA) y las pruebas están en una sola rama. Ahora revisarás el conjunto y abrirás una solicitud de incorporación de cambios (PR). Combinaste manualmente la PR de las valoraciones; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> En condiciones normales, dividiríamos la funcionalidad, las instrucciones, la habilidad y el agente de QA en varias PR. Para simplificar el taller, todo el flujo de trabajo de filtrado y calidad está en una rama y se incluirá en una sola PR.

En esta lección:

- aprenderás cómo Agent Merge automatiza el ciclo de una PR.
- revisarás el cambio completo y las pruebas de verificación.
- crearás la PR de filtrado.
- activarás Agent Merge después de la revisión y confirmarás la combinación.

## Escenario

Has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la PR, pero mantener bajo control del desarrollador la autorización para combinarla.

## Acerca de Agent Merge

**Agent Merge** automatiza el trabajo necesario para incorporar una PR desde Copilot CLI. El agente puede resolver comprobaciones de integración continua (CI) fallidas y comentarios de revisión, rebasar la rama y activar la combinación automática de GitHub cuando el repositorio lo permita.

Hasta ahora has seleccionado **Merge pull request** manualmente. Revisa el trabajo antes de permitir que Agent Merge se encargue del proceso.

## Utiliza Agent Merge para gestionar la PR

Revisa el estado completo de la rama y crea la solicitud antes de permitir que Agent Merge se encargue del proceso.

1. Vuelve al codespace y revisa `/diff` y las pruebas de verificación.
2. Ejecuta `/agent` y selecciona **Default**.
3. Crea una PR con `/pr create`.
4. Activa Agent Merge con:

   ```plaintext
   /pr agentmerge
   ```

5. Sigue el proceso de integración continua y revisa los comentarios. Cuando todo esté listo, el agente combinará la PR.
6. Confirma que Copilot informa de una combinación correcta, por ejemplo, `PR #14 was squash-merged successfully`.

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, las protecciones de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, revisa el motivo y combina manualmente la PR después de revisarla, si el repositorio lo permite.

## Resumen y pasos siguientes

Has:

- aprendido cómo Agent Merge automatiza el ciclo de una PR.
- revisado el cambio completo y las pruebas de verificación.
- creado la PR de filtrado.
- activado Agent Merge después de la revisión y confirmado que se combinó.

A continuación, [explorarás comandos de barra útiles de Copilot CLI][next-lesson] para gestionar el contexto, los modelos, el uso compartido y la delegación opcional en la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
