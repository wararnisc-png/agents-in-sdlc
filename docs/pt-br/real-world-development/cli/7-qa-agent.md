---
title: "Lição 7 - Crie e use um agente de QA"
description: "Crie um agente de QA personalizado que combine requisitos da issue, a skill quality-checks e o MCP do Playwright."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você usou a skill `quality-checks` para executar verificações automatizadas e o MCP do Playwright para observar a experiência de filtragem no navegador. Agora, combinará esses recursos em um agente personalizado com um processo de QA bem definido.

Nesta lição, você vai:

- explorar como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criar e inspecionar um perfil reutilizável de garantia da qualidade;
- selecionar o agente de QA e revisar as descobertas em relação à issue de filtragem.

## Cenário

Antes da abertura de um pull request (PR), a Tailspin Toys quer revisar de forma consistente os requisitos, a qualidade do código, as verificações automatizadas, a cobertura de testes e o comportamento no navegador. Um agente personalizado pode coordenar esse processo de QA e gerar um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot, definida em um perfil Markdown. O perfil descreve o objetivo do agente, suas instruções e as ferramentas disponíveis. Neste workshop, você definirá a função de QA em `.github/agents/qa.agent.md` e a selecionará no Copilot CLI.

As personalizações usadas até agora têm funções distintas. As instruções do repositório descrevem os padrões da equipe. A skill `quality-checks` reúne verificações repetíveis. O MCP do Playwright fornece ferramentas para o navegador. O perfil de QA orienta o Copilot sobre como usar esses recursos para avaliar os requisitos e relatar as descobertas. Ele não substitui os outros recursos nem exige outra conversa.

## Crie o perfil de QA

Antes de abrir o PR da funcionalidade, peça ao Copilot para criar um perfil de QA reutilizável. O perfil definirá tanto as verificações que o QA executará quanto os limites que precisará respeitar.

1. Volte ao Codespace e confirme se a conversa sobre filtragem está no modo Interactive.
2. Peça ao agente padrão para criar o novo agente personalizado:

   ```plaintext
   Crie um agente personalizado chamado QA em .github/agents/qa.agent.md. Ele deve verificar as funcionalidades de acordo com as issues e os requisitos acordados, seguir as instruções do repositório, executar a skill quality-checks, usar o MCP do Playwright para verificar o comportamento e adicionar testes quando a cobertura estiver incompleta.

   Peça que ele classifique cada requisito como aprovado, reprovado ou bloqueado e forneça evidências. Ele deve pedir autorização antes de alterar o código de implementação e não pode confirmar alterações nem abrir pull requests.

   Por enquanto, apenas crie o perfil para que eu possa revisá-lo.
   ```

## Inspecione o perfil

Antes de usar o novo agente, revise o perfil para confirmar se o Copilot registrou o fluxo de QA e os limites pretendidos. Isso evita que um agente incompleto ou com escopo amplo demais altere a funcionalidade quando você só quer verificá-la.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. O campo `description` é obrigatório; `name` é opcional, mas, se for incluído, oferecerá ao agente um nome de exibição claro.
3. Leia as instruções do perfil e confirme se o agente de QA começa pelos requisitos, segue as instruções do repositório, executa a skill `quality-checks` e usa o MCP do Playwright.
4. Confirme se o agente de QA fornece evidências, pede autorização antes de alterar o código de implementação e não confirma alterações nem abre pull requests.
5. Se o perfil gerado não incluir alguma dessas responsabilidades ou limites, peça ao agente padrão para revisá-lo antes de continuar.

## Execute o QA com base na issue

O Copilot CLI carrega os agentes do projeto no início de uma conversa. Retome a mesma conversa sobre a filtragem depois de criar o perfil e selecione o agente de QA para que ele possa usar a issue e as decisões de planejamento já presentes no contexto.

1. Ative o agente com este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como você acabou de criar o agente, talvez ele ainda não apareça na lista de agentes disponíveis. Mesmo assim, o comando acima o ativará.

2. Use o prompt a seguir para pedir que o agente de QA revise a funcionalidade:

   ```plaintext
   Revise a funcionalidade de filtragem de acordo com a issue e as decisões do nosso plano. Ela está pronta para um PR?
   ```

3. O agente de QA começará a trabalhar.
4. Depois que terminar, leia o relatório apresentado.

## Resumo e próximos passos

Você adicionou uma função especializada reutilizável ao fluxo de trabalho e revisou o resultado. Nesta lição, você:

- explorou como um agente personalizado trabalha com instruções, skills e ferramentas MCP;
- criou e inspecionou um perfil reutilizável de garantia da qualidade;
- selecionou o agente de QA e revisou as descobertas em relação à issue de filtragem.

Agora você tem a implementação, a atualização da skill, o perfil de QA, os testes e o relatório de verificação prontos para revisão. Em seguida, você [reunirá esses itens em um PR da funcionalidade e usará o Agent Merge][next-lesson].

## Recursos

- [Criar agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
