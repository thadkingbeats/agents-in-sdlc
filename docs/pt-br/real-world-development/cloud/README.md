---
slug: pt-br/real-world-development/cloud
title: "Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

O **[agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** permite que o GitHub Copilot trabalhe de forma assíncrona na nuvem. Você atribui uma tarefa no GitHub, e o agente de nuvem a executa em segundo plano — explorando o repositório, fazendo alterações e abrindo uma pull request — enquanto você se dedica a outras atividades.

Nestes exercícios, você adicionará instruções personalizadas para o agente de nuvem e, em seguida, atribuirá um problema do GitHub para que ele implemente o trabalho. Você revisará e usará agentes personalizados para orientar a abordagem, acompanhará e direcionará sessões pelo painel de agentes e, por fim, revisará as pull requests e fará iterações sobre os resultados.

## Exercícios

| Exercício | Tópico | Descrição |
|----------|-------|-----------|
| [0. Pré-requisitos][ex0] | Configuração | Crie seu repositório e um codespace |
| [1. Instruções personalizadas][ex1] | Contexto | Adicione instruções personalizadas para o agente de nuvem |
| [2. Agente de nuvem][ex2] | Agente assíncrono | Atribua problemas ao agente de nuvem do Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revise e use agentes personalizados |
| [4. Gerenciamento de agentes][ex4] | Monitoramento | Acompanhe e direcione sessões do agente |
| [5. Iteração][ex5] | Revisão | Revise pull requests, faça iterações no trabalho do Copilot e escolha os próximos passos |

## Pré-requisitos

Antes deste workshop, verifique se você tem:

- [ ] Uma conta do GitHub com um plano **Copilot Student, Pro, Pro+, Business ou Enterprise** ativo
- [ ] O agente de nuvem do Copilot habilitado para sua conta ou organização

> [!TIP]
> Não tem um plano pago? Estudantes com status verificado podem obter o GitHub Copilot gratuitamente pelo [GitHub Education][callout-student-plan-education]. O plano **Copilot Student** inclui o agente, o Model Context Protocol (MCP), revisão de código e os recursos do Copilot CLI usados neste workshop — você pode concluir todos os ambientes com esse plano.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> O agente de nuvem está disponível nos planos **Copilot Student, Pro, Pro+, Business e Enterprise** — em todos, exceto no Copilot Free. No Copilot Business ou Enterprise, um administrador precisa habilitá-lo para a organização.

> [!NOTE]
> Este ambiente não aborda o Model Context Protocol (MCP). Para explorar o uso de servidores MCP com o Copilot, consulte o [ambiente do CLI](../cli/) ou o [ambiente do VS Code](../vscode/).

## Comece

**[Comece pelo Exercício 0: pré-requisitos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
