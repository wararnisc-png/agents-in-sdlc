---
title: "Lição 12 - Publique o site com o GitHub Pages"
description: "Use o aplicativo GitHub Copilot para configurar um fluxo de trabalho do Pages, revisar o pull request e verificar o Space Quiz publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Dê ao Space Quiz um endereço público publicando-o com o GitHub Pages. O Copilot pode preparar o fluxo de trabalho e orientar a publicação, mas você continua responsável por revisar as mudanças e confirmar que o site está disponível.

Nesta lição, você vai:

- pedir ao Copilot para configurar uma publicação no GitHub Pages.
- revisar o fluxo de trabalho e o pull request antes da mesclagem.
- acompanhar a publicação e verificar o site publicado.

## Cenário

O Space Quiz já está em um repositório do GitHub, mas as pessoas ainda precisam de uma forma simples de experimentá-lo. Publicar o site de arquivo único com o GitHub Pages o disponibiliza em uma URL pública, sem adicionar um servidor ou dependência de runtime.

## Peça ao Copilot para preparar a publicação

> [!WARNING]
> Criar um pull request pode confirmar e enviar código. Revise as configurações de aprovação e o repositório de destino antes de enviar este prompt. Com **Aprovar tudo**, não espere uma solicitação de confirmação separada.

Na sessão do aplicativo Copilot para `space-quiz`, envie este prompt:

```plaintext
Prepare uma implantação do GitHub Pages para este repositório. Crie um fluxo de trabalho do GitHub Actions que compile o site, se necessário, e o implante no GitHub Pages depois que as alterações chegarem à branch padrão. Adicione um README que descreva o aplicativo e como executá-lo localmente, caso ainda não exista. Crie um pull request com essas alterações e informe o link e quaisquer configurações ou permissões necessárias do Pages. Não faça a mesclagem, não habilite a mesclagem automática, não altere as configurações do Pages e não publique o site. Pare e aguarde minha revisão.
```

## Revise o fluxo de trabalho e o pull request

1. Confirme se o README só foi adicionado caso o repositório ainda não tivesse um.
2. Revise as alterações do pull request, incluindo as etapas de compilação e publicação do fluxo de trabalho, os gatilhos e as permissões.
3. Confirme se o fluxo de trabalho publica a partir da branch padrão, e não de um pull request ainda não mesclado.
4. Solicite correções, se necessário, e revise o diff atualizado. Aguarde a aprovação nas verificações obrigatórias do pull request antes de autorizar a mesclagem.

## Autorize a mesclagem e a publicação

> [!WARNING]
> O prompt a seguir autoriza o agente a mesclar o pull request revisado, alterar as configurações do Pages do repositório e publicar o site. Envie-o somente depois de concluir a revisão e confirmar o repositório e o pull request. As configurações de aprovação podem permitir essas ações sem outra confirmação.

Substitua `<PR_NUMBER>` pelo número do pull request que você revisou e envie este prompt separado:

```plaintext
Revisei o pull request <PR_NUMBER> neste repositório e autorizo a mesclagem e a publicação. Habilite o GitHub Pages usando o GitHub Actions, mescle somente esse pull request depois que as verificações obrigatórias forem aprovadas e acompanhe a publicação até ela ser concluída com êxito. Informe a URL final do site publicado. Se você não tiver permissão para habilitar o Pages ou mesclar, diga exatamente o que preciso aprovar ou fazer; não informe sucesso até que o site esteja disponível.
```

![Diagrama em três etapas: um pull request de space-quiz mesclado; uma execução bem-sucedida do GitHub Actions para publicar o site, com as etapas Build website, Upload artifact e Deploy to Pages; e o Space Quiz publicado em yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Verifique a publicação

1. Acompanhe a execução de publicação do GitHub Actions até que ela seja concluída com êxito.
2. Abra a URL informada e confirme se o Space Quiz carrega.

Se o agente não puder habilitar o Pages ou mesclar o pull request, siga as instruções específicas que ele fornecer. Não considere a tarefa concluída até que a publicação tenha sido bem-sucedida e o site esteja carregando.

## Resumo e próximos passos

Agora o Space Quiz está disponível como um site publicado, e você verificou a publicação em vez de confiar apenas no relato do agente. Continue para [Lição 13: Revisão e próximos passos][next-lesson].

[next-lesson]: ../13-review/
