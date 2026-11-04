---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Defina uma abordagem com Plan, implemente a filtragem de uma issue com Autopilot e revise o resultado no modo Interactive."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você começou adicionando um pequeno recurso ao projeto. Alterações maiores exigem um processo mais completo. O GitHub Copilot CLI pode seguir o fluxo de trabalho existente da equipe para ajudar a criar os recursos certos da maneira adequada. Nesta lição e nas seguintes, você seguirá um processo de desenvolvimento com agentes: começará por uma issue, criará um recurso, verificará o código e o comportamento e, por fim, fará o merge no projeto.

> [!NOTE]
> Você usará a mesma conversa e branch durante o fluxo de trabalho do recurso. Normalmente, haveria branches ou PRs diferentes para cada tipo de arquivo, mas este workshop reúne o trabalho para manter o foco nos conceitos principais.

Nesta lição, você vai:

- iniciar uma conversa do Copilot a partir de uma issue do GitHub;
- definir requisitos no modo Plan;
- implementar o recurso no modo Autopilot;
- revisar o código;
- validar manualmente o recurso em um navegador encaminhado.

Ao continuar o trabalho, você atualizará as instruções do repositório, personalizará a skill `quality-checks`, adicionará a validação MCP, criará um agente de QA e abrirá a PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar jogos por categoria e editora. A issue do backlog descreve o recurso, mas decisões como a combinação de categorias precisam ser acordadas antes de começar a programar. Use o modo Plan para resolver essas questões e, depois, autorize uma implementação com escopo definido pelo Autopilot.

## Contexto

A inclusão de agentes de programação com inteligência artificial no fluxo de desenvolvimento não muda seus fundamentos. A maioria das equipes segue um processo semelhante:

1. Começar por uma issue registrada que descreva o trabalho.
2. Planejar o que será criado.
3. Criar e revisar o código.
4. Executar testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar uma pull request (PR).
7. Mesclar o código depois da revisão e da aprovação da integração contínua.

> [!NOTE]
> Os detalhes variam de acordo com a equipe e a organização, mas a maioria dos processos segue uma variação dessas etapas.

Esse processo ajuda a garantir que o código gerado por inteligência artificial atenda aos requisitos e passe pelas mesmas verificações que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere alterações e espera sua orientação antes de continuar.
- **Plan**: o agente cria um plano e não pode editar arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma, escreve código, executa testes e itera até concluir a tarefa.

Comece no modo Plan, revise o plano e use o modo Autopilot para implementá-lo.

## Comece pela issue

Antes de iniciar o trabalho de filtragem, volte ao codespace e prepare o repositório e o terminal.

1. Volte ao codespace. Se estiver parado, reinicie-o.
2. Confirme se a PR de avaliações por estrelas foi mesclada.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para a filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para exibir todas as issues.
8. Use as setas para selecionar a issue **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

Observe que o prompt começa com `#7` ou um número semelhante. O prefixo `#` adiciona ao contexto uma issue ou pull request do GitHub.

## Planeje o recurso de filtragem

O planejamento permite definir a abordagem antes de pedir ao Copilot que implemente o recurso ou execute uma tarefa. É recomendável planejar tarefas complexas.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar para o modo Plan. Confirme se o indicador abaixo do prompt exibe **Plan**.
2. Depois da referência à issue adicionada na etapa anterior, digite:

   ```plaintext
   Create a plan for implementing this feature.
   ```

O Copilot explorará o projeto e definirá uma abordagem. Durante o processo, ele talvez pergunte como a filtragem deve funcionar. Responda de acordo com suas preferências.

1. Quando o plano estiver pronto, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
2. Percorra o plano e revise-o.
3. Peça ao Copilot que revise qualquer parte que não corresponda às decisões tomadas.

## Aprove o Autopilot

Com o plano escrito e revisado, implemente-o usando o Autopilot, que permite ao Copilot iterar até considerar a tarefa concluída.

1. Selecione **Accept plan and build on autopilot (recommended)** ou uma opção com nome semelhante na versão instalada.
2. Confirme se o indicador de modo abaixo do prompt exibe **Autopilot**.
3. Acompanhe o Copilot executar o plano, gerar código e rodar testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente; revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revise e verifique a implementação

Assim como qualquer outro código, o código gerado precisa ser revisado antes do merge.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme se o indicador não exibe **Plan** nem **Autopilot**.
2. Digite `/diff` e examine a implementação da filtragem e os testes.
3. Compare o resultado com a issue e com as decisões tomadas durante o planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da visualização de diff.
5. Revise os resultados das verificações do projeto e peça ao Copilot que corrija eventuais falhas.

## Explore a nova funcionalidade

Inicie o aplicativo e abra o site pela porta encaminhada pelo Codespaces para verificar se o código funciona.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Teste os filtros de categoria, os filtros de editora e as combinações acordadas no plano.
4. Confirme se a redefinição dos filtros e os resultados vazios correspondem à issue e às suas decisões.
5. Volte ao codespace e peça ao Copilot que pare o servidor de desenvolvimento iniciado.

## Resumo e próximos passos

Você usou diferentes modos de conversa para criar e revisar um recurso. Nesta lição, você:

- iniciou uma conversa do Copilot a partir de uma issue do GitHub;
- definiu os requisitos no modo Plan;
- implementou o recurso no modo Autopilot;
- revisou o código;
- validou manualmente o recurso em um navegador encaminhado.

Em seguida, [use instruções personalizadas][next-lesson] para garantir que o código siga os padrões documentados.

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
