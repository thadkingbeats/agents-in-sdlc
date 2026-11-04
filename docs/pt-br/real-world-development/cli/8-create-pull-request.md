---
title: "Lição 8 - Crie e mescle a PR do recurso"
description: "Revise a filtragem, as instruções, a skill, o perfil de QA e os testes; crie uma PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as atualizações das instruções, a atualização da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em uma única branch. Agora, revise tudo em conjunto e abra uma pull request. Você mesmo fez o merge da PR de avaliações por estrelas; desta vez, deixe o **Agent Merge** gerenciar o processo.

> [!NOTE]
> Normalmente, dividiríamos o recurso, as atualizações de instruções, a atualização da skill e o agente de QA em algumas PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma conversa e branch e incluiremos o trabalho nesta PR.

Nesta lição, você vai:

- conhecer o Agent Merge e como ele automatiza o ciclo de merge;
- examinar todas as alterações do recurso e as evidências de verificação;
- criar a PR de filtragem;
- habilitar o Agent Merge somente depois da revisão e confirmar o merge da PR.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. Agora, a Tailspin Toys quer automatizar o trabalho restante da PR, mantendo a autorização do merge sob o controle da pessoa desenvolvedora.

## Conheça o Agent Merge

O **Agent Merge** automatiza o trabalho restante para integrar uma pull request. Quando habilitado, o Copilot resolve os impedimentos da PR: corrige verificações de integração contínua (CI) com falha, responde aos comentários de revisão e faz rebase quando necessário. Em seguida, habilita o merge automático do GitHub, se o repositório permitir.

Até agora, você selecionou **Merge pull request**. O Agent Merge pode cuidar dessa etapa. Revise o trabalho e confirme se está pronto antes de habilitar o Agent Merge.

## Use o Agent Merge para gerenciar a PR

Com o código pronto, revise-o, crie a PR e deixe o Agent Merge gerenciar o restante do processo.

1. Volte ao codespace.
2. Abra a caixa de diálogo de agentes digitando `/agent`.
3. Na lista de opções, selecione **Default** e pressione <kbd>Enter</kbd>.
4. Crie uma PR com o comando `/pr create`.
5. Ative o Agent Merge com `/pr agentmerge`.
6. O Copilot acompanhará a integração contínua da PR e fará o merge quando tudo for aprovado.
7. Confirme se o Copilot informa algo semelhante a `PR #14 was squash-merged successfully`.

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de merge, configurações do repositório nem permissões ausentes. Se o processo for bloqueado, leia o motivo informado e, quando o repositório permitir, faça manualmente o merge após a revisão.

## Resumo e próximos passos

Você automatizou várias etapas do desenvolvimento: geração de código, testes e validação e, agora, o processo da pull request. Você:

- conheceu o Agent Merge e como ele automatiza o ciclo de merge;
- examinou todas as alterações do recurso e as evidências de verificação;
- criou a PR de filtragem;
- habilitou o Agent Merge somente após a revisão e confirmou o merge da PR.

Em seguida, [explore outros comandos de barra do Copilot CLI][next-lesson] para gerenciar contexto, modelos e compartilhamento e, se quiser, delegar tarefas à nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
