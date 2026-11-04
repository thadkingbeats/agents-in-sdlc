---
title: "Lição 2 - Adicione avaliações por estrelas: uma melhoria rápida"
description: "Use o Copilot CLI para alterar os cards de jogos, revisar a mudança no navegador encaminhado e integrar sua primeira pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e iniciou uma conversa, faça sua primeira alteração no projeto. Mantenha-a pequena: os jogos já têm uma avaliação por estrelas nos dados, mas os cards da página inicial ainda não a exibem. Peça ao agente que mostre a avaliação, revise a alteração e faça o merge da primeira pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em uma branch de recurso;
- pedir ao agente que faça uma pequena alteração no projeto;
- revisar a alteração com `/diff`;
- executar o aplicativo e verificar a mudança no navegador encaminhado;
- abrir e mesclar sua primeira pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação por estrelas, que já aparece na página de detalhes. Os cards da página inicial mostram apenas o título, a categoria, a editora e a descrição. Como primeiro exercício, peça ao agente que exiba em cada card a avaliação existente: uma alteração pequena e independente, ideal para sua primeira sessão.

## Estrutura de uma conversa

Uma **conversa** é o espaço em que você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal do CLI usa o repositório e a branch atualmente selecionados no terminal, em vez de criar uma worktree dedicada. As conversas salvas permitem retomar a discussão; os arquivos e a branch continuam sendo o estado normal do Git no disco.

Em uma conversa, você verá os prompts e as respostas, a atividade das ferramentas do agente enquanto ele explora e edita arquivos e as alterações que pode inspecionar com `/diff`.

## Inicie uma conversa e solicite a alteração

Inicie uma conversa para implementar o recurso.

1. Volte ao codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Se o Copilot ainda não estiver em execução, use este comando:

   ```bash
   copilot --yolo
   ```

4. Inicie uma sessão nova com `/new` e pressione <kbd>Enter</kbd>.
5. Solicite a alteração com este prompt:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

O Copilot explorará o projeto, localizará os arquivos que exibem os detalhes dos jogos e criará o código necessário. Você adicionou um recurso com o Copilot CLI.

## Revise o diff

Revise todas as alterações geradas por inteligência artificial antes de mesclá-las, mesmo quando forem pequenas.

1. Digite `/diff` e examine todos os arquivos alterados.
2. Confirme se o card mostra a avaliação numérica quando ela existe e `No rating yet` quando `starRating` é `null`.
3. Confirme se os testes abrangem os dois casos.
4. Revise os resultados das verificações executadas pelo Copilot e peça que ele corrija as falhas.
5. Quando terminar a revisão, pressione <kbd>Esc</kbd> para sair da tela de diff.

> [!NOTE]
> Como todas as ferramentas de inteligência artificial generativa, o Copilot é probabilístico. O código exato pode variar. Revise o comportamento, sem esperar uma implementação idêntica.

## Verifique as alterações

Não basta ler o código e presumir que funciona. Peça ao Copilot que inicie o site para que você examine a interface no navegador encaminhado pelo Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme se os cards dos jogos mostram as avaliações em uma escala de cinco estrelas.
4. Volte ao Copilot e peça que pare o servidor iniciado:

   ```plaintext
   Stop the development server you started.
   ```

## Abra e mescle sua primeira pull request

Agora que criou o recurso, abra uma pull request (PR) para integrá-lo ao projeto.

1. Peça ao agente padrão que faça commit da alteração:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Digite `/pr create`. Ao criar a PR, o Copilot CLI enviará o commit existente e exibirá a URL da PR.
3. Para abrir a PR, mantenha pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecione a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver tudo pronto, selecione **Merge pull request** e confirme o merge.
6. Volte ao codespace e saia do Copilot CLI com `/exit`.
7. Atualize sua branch local `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Você entregou sua primeira alteração com o GitHub Copilot CLI. Você:

- iniciou uma conversa focada do Copilot em uma branch de recurso;
- orientou o agente a fazer uma pequena alteração nos cards de jogos;
- revisou a alteração com `/diff`;
- executou o aplicativo e verificou a avaliação no navegador encaminhado;
- abriu e mesclou sua primeira pull request.

Em seguida, [comece pela issue de filtragem e use os modos Plan e Autopilot][next-lesson] para criar um recurso maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
