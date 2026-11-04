---
title: "Exercício 2 - Adicionar funcionalidades com o modo de agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo uma atualização simples de um aplicativo pode exigir alterações em vários arquivos e a execução de testes. Normalmente, uma pessoa desenvolvedora localiza os arquivos necessários, faz as alterações, executa os testes, depura problemas, encontra arquivos que faltaram e repete o processo.

O modo de agente do Copilot ajuda a realizar esse trabalho no IDE. Ele explora a estrutura do projeto, faz as alterações necessárias, executa tarefas como testes e corrige problemas encontrados. Neste exercício, você usará o modo de agente para adicionar uma funcionalidade ao site.

> [!NOTE]
> Embora os nomes sejam parecidos, o modo de agente e o agente de nuvem oferecem experiências diferentes. O modo de agente trabalha no IDE, com ciclos rápidos de feedback e interação. O agente de nuvem funciona de maneira assíncrona, como uma pessoa da equipe, e interage por meio de issues e pull requests.

Neste exercício, você vai aprender a:

- usar o modo de agente para explorar o projeto, identificar arquivos relevantes e coordenar alterações;
- implementar recursos na interface e na camada de dados;
- revisar as alterações e os testes gerados antes do merge.

## Cenário

À medida que a lista de jogos cresce, você quer permitir que as pessoas filtrem os jogos por categoria e editora. No exercício anterior, você adicionou um auxiliar de editoras. Agora, concluirá com o modo de agente as alterações restantes na camada de dados, na interface e nos testes.

## Execute o site Tailspin Toys

Antes de fazer alterações, explore o site para entender suas funcionalidades atuais.

O site é uma plataforma de financiamento coletivo para jogos de tabuleiro com tema de desenvolvimento. Ele permite listar jogos e exibir detalhes. O site é um único aplicativo Astro, que gera páginas HTML estáticas durante a compilação. As páginas consultam diretamente um banco de dados SQLite local por meio do mapeador objeto-relacional (ORM) Drizzle no frontmatter; não há uma interface de programação de aplicações (API) de back-end separada nem um framework de interface no cliente. Os auxiliares reutilizáveis de acesso a dados ficam em `src/lib/`. A interatividade é implementada com scripts Astro pequenos e específicos, usando APIs padrão do Document Object Model (DOM).

### Inicie o site

O projeto oferece a tarefa `npm run dev`, que inicia o servidor de desenvolvimento Astro.

1. Volte ao codespace. Você deverá estar em `main` depois do exercício anterior.
2. Abra um terminal no codespace com <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

   Quando o servidor Astro estiver pronto, será exibido um aviso com a URL, semelhante a:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se uma caixa de diálogo solicitar a abertura de `http://localhost:4321` em um navegador, feche-a selecionando **x**.

1. Para abrir o site, mantenha pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecione o endereço do servidor Astro `http://localhost:4321` no terminal.

> [!NOTE]
> Em um codespace, selecionar o link `localhost` no terminal redireciona automaticamente para `https://<your-codespace-name>-4321.app.github.dev/`, um túnel privado para o servidor do codespace.

### Explore o site

Com o site em execução, explore suas funcionalidades:

- **Página inicial**: exibe uma lista de jogos de tabuleiro com títulos, imagens e descrições.
- **Página de detalhes do jogo**: ao selecionar um jogo, você verá mais informações, como título, descrição, editora e categoria.

## Explore o backlog com o Copilot

> [!TIP]
> **Abra o Copilot Chat**
>
> Antes de começar as etapas abaixo, volte ao codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa informa o que selecionar quando necessário.

O site já funciona, mas você quer adicionar recursos. Comece examinando o backlog de issues criado automaticamente quando o projeto foi copiado do modelo.

1. Na visualização Chat, selecione **Agent** no menu suspenso de agentes. O agente planeja e implementa alterações em vários arquivos, executa comandos no terminal e usa ferramentas.

   ![Seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

2. Na lista de modelos disponíveis, selecione **Claude Sonnet 4.5**.

> [!CAUTION]
> A inclusão de **Claude Sonnet 4.5** não indica uma preferência por um modelo específico. Esse foi o modelo usado ao preparar o workshop para manter as sugestões relativamente consistentes. Como os modelos de linguagem são probabilísticos, as sugestões podem ser diferentes das descritas aqui; isso é normal.

> [!NOTE]
> Devido à natureza probabilística dos modelos de linguagem, o Copilot pode usar um comando MCP diferente e ainda assim concluir a tarefa.

1. Envie ao Copilot este prompt para consultar o backlog:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

2. Selecione **Continue** para executar o comando que lista as issues.
3. Revise a lista gerada.

Observe como o Copilot priorizou os itens de acordo com o que considera mais útil para as pessoas usuárias.

## Revise os arquivos de instruções

Antes de pedir ao agente que gere código, examine o arquivo de instruções que fornecerá contexto. O arquivo [de instruções para a interface do usuário](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md) explica como adicionar funcionalidades ao site.

1. No codespace, abra `.github/instructions/ui.instructions.md`.
2. Observe as orientações gerais para adicionar funcionalidades, incluindo:
   - uma visão geral da arquitetura;
   - princípios de design de componentes, testabilidade e acessibilidade;
   - links para instruções específicas de tipos de arquivo, incluindo Astro, Tailwind CSS e Drizzle.

> [!TIP]
> Os arquivos de instruções podem apontar para outros arquivos de instruções e arquivos do projeto. Os caminhos são relativos ao arquivo de instruções, permitindo reutilizar conteúdo, dividir instruções complexas em partes menores e fornecer exemplos e modelos.

## Implemente a filtragem

Para concluir a filtragem, o aplicativo precisa de pelo menos três alterações:

- adicionar ou aprimorar a lógica de filtragem na camada de dados (`src/lib/`);
- adicionar ou atualizar testes do comportamento de filtragem;
- atualizar a página de listagem de jogos com a interface de filtragem.

Os testes também precisam ser executados e aprovados antes do merge. O modo de agente do Copilot pode executar essas tarefas.

1. Continue na conversa atual com o Copilot ou selecione **New Chat** para iniciar outra.
2. Selecione **Add Context**, **Instructions** e **ui** para adicionar o arquivo de instruções.

   ![Exemplo de seleção do arquivo de instruções da interface](../../../_images/ex3-select-instructions-file.png)

3. Confirme se **Agent** está selecionado no menu suspenso de agentes.

   ![Seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirme se **Claude Sonnet 4.5** continua selecionado como modelo.
5. Peça ao Copilot que implemente a funcionalidade conforme a issue relacionada no backlog:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observe o Copilot explorar o projeto, localizar os auxiliares da camada de dados, a interface e os testes, alterar os arquivos e executar os testes.

   ![Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot executará várias tarefas, como explorar o projeto, alterar arquivos e executar testes. Isso pode levar alguns minutos. Enquanto trabalha, ele pode exibir os controles **Keep** e **Undo** no editor. Quando terminar, haverá um controle para manter ou desfazer cada alteração; não é necessário selecioná-los durante o trabalho.

1. Quando o Copilot solicitar, selecione **Continue** para executar os testes.

   ![Caixa de diálogo do Copilot Chat solicitando confirmação para executar os testes](../../../_images/ex3-agent-mode-run-tests.png)

2. Talvez haja pausas e falhas em alguns testes durante o processo. O Copilot alterna entre gerar código e executar testes até concluir a tarefa sem detectar erros.

   ![Sessão completa do Copilot Chat no modo de agente](../../../_images/ex3-agent-mode-proposed-changes.png)

3. Examine o código gerado para detectar possíveis problemas.

> [!CAUTION]
> Sempre revise o código gerado pelo Copilot ou por outras ferramentas de inteligência artificial.

1. Volte ao navegador em que o site está em execução e explore a nova funcionalidade.
2. Depois de confirmar que tudo funciona e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximos passos

Você usou o modo de agente do GitHub Copilot para adicionar funcionalidades ao site Tailspin Toys. Você aprendeu a:

- implementar recursos na interface e na camada de dados com o modo de agente;
- explorar o projeto, identificar arquivos relevantes e coordenar alterações;
- revisar as alterações e os testes gerados antes do merge.

Agora, [teste a funcionalidade com o servidor MCP do Playwright][next-lesson] e abra uma pull request.

### Exercício extra de exploração — implemente paginação

À medida que a lista de jogos crescer, será necessário adicionar paginação. Use as habilidades deste exercício e peça ao Copilot que implemente a paginação. Considere:

- seguir as práticas recomendadas existentes, inclusive usar os arquivos de instruções;
- decidir se as pessoas poderão escolher o tamanho da página ou se ele será fixo;
- fornecer ao Copilot as orientações necessárias no prompt;
- iterar com o GitHub Copilot, solicitando alterações e fornecendo contexto. Esse processo é normal ao trabalhar com o Copilot.

## Recursos

- [Modos Ask, Edit e Agent do Copilot: o que fazem e quando usar cada um][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
