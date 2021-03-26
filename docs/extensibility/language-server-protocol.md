---
title: Visão geral do protocolo de servidor de linguagem | Microsoft Docs
description: Saiba mais sobre como o protocolo de servidor de linguagem fornece uma estrutura útil para expor recursos de linguagem a uma variedade de ferramentas.
ms.custom: SEO-VS-2020
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5dd212b5f75679b44175d9b160d3e11d2075d6a5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074021"
---
# <a name="language-server-protocol"></a>Language Server Protocol

## <a name="what-is-the-language-server-protocol"></a>O que é o protocolo de servidor de linguagem?

Dar suporte a recursos de edição avançados como preenchimentos automáticos de código-fonte ou **ir para a definição** de uma linguagem de programação em um editor ou IDE é tradicionalmente desafiador e demorado. Normalmente, ele requer a gravação de um modelo de domínio (um scanner, um analisador, um verificador de tipo, um construtor e muito mais) na linguagem de programação do editor ou do IDE. Por exemplo, o plug-in Eclipse CDT, que fornece suporte para C/C++ no IDE do eclipse, é escrito em Java, já que o próprio IDE do eclipse é escrito em Java. Seguindo essa abordagem, isso significaria implementar um modelo de domínio C/C++ em TypeScript para Visual Studio código e um modelo de domínio separado em C# para Visual Studio.

Criar modelos de domínio específicos de idioma também será muito mais fácil se uma ferramenta de desenvolvimento puder reutilizar bibliotecas específicas de idioma existentes. No entanto, essas bibliotecas são geralmente implementadas na linguagem de programação em si (por exemplo, bons modelos de domínio C/C++ são implementados em C/C++). A integração de uma biblioteca C/C++ em um editor escrito em TypeScript é tecnicamente possível, mas difícil de fazer.

### <a name="language-servers"></a>Servidores de idiomas

Outra abordagem é executar a biblioteca em seu próprio processo e usar a comunicação entre processos para conversar com ela. As mensagens enviadas de volta e para trás formam um protocolo. O LSP (protocolo de servidor de linguagem) é o produto de padronização das mensagens trocadas entre uma ferramenta de desenvolvimento e um processo de servidor de idioma. Usar servidores de idiomas ou Demons não é uma ideia nova ou romance. Editores como vim e Emacs têm feito isso por algum tempo para fornecer suporte de preenchimento automático semântico. O objetivo do LSP era simplificar esses tipos de integrações e fornecer uma estrutura útil para expor recursos de linguagem a uma variedade de ferramentas.

Ter um protocolo comum permite a integração de recursos de linguagem de programação em uma ferramenta de desenvolvimento com um mínimo de confusão ao reutilizar uma implementação existente do modelo de domínio da linguagem. Um back-end de servidor de linguagem pode ser escrito em PHP, Python ou Java e o LSP permite que ele seja facilmente integrado a uma variedade de ferramentas. O protocolo funciona em um nível comum de abstração para que uma ferramenta possa oferecer serviços de linguagem avançados sem a necessidade de compreender totalmente as nuances específicas ao modelo de domínio subjacente.

## <a name="how-work-on-the-lsp-started"></a>Como o trabalho no LSP foi iniciado

O LSP evoluiu ao longo do tempo e hoje está na versão 3,0. Ele começou quando o conceito de um servidor de linguagem foi obtido pelo OmniSharp para fornecer recursos de edição avançados para C#. Inicialmente, o OmniSharp usava o protocolo HTTP com uma carga JSON e foi integrado a vários editores, incluindo [Visual Studio Code](https://code.visualstudio.com).

Ao mesmo tempo, a Microsoft começou a trabalhar em um servidor de linguagem TypeScript, com a ideia de dar suporte ao TypeScript em editores como o texto Emacs e sublime. Nessa implementação, um editor se comunica por meio de stdin/stdout com o processo do servidor TypeScript e usa uma carga JSON inspirada pelo protocolo do depurador V8 para solicitações e respostas. O servidor TypeScript foi integrado ao plug-in sublime do TypeScript e VS Code para edição do TypeScript rica.

Depois de ter integrado dois servidores de idiomas diferentes, a equipe de VS Code começou a explorar um protocolo de servidor de linguagem comum para editores e IDEs. Um protocolo comum permite que um provedor de linguagem crie um único servidor de linguagem que pode ser consumido por IDEs diferentes. Um consumidor de servidor de linguagem precisa apenas implementar o lado do cliente do protocolo uma vez. Isso resulta em uma situação de Win-Win para o provedor de idioma e o consumidor do idioma.

O protocolo de servidor de idioma foi iniciado com o protocolo usado pelo servidor TypeScript, expandindo-o com mais recursos de linguagem inspirados pela API de linguagem de VS Code. O protocolo é apoiado com JSON-RPC para invocação remota devido à sua simplicidade e às bibliotecas existentes.

A equipe de VS Code protótipou o protocolo implementando vários servidores de linguagem mais pano que respondem a solicitações para fazer um pano sem fiapos (examinar) um arquivo e retornar um conjunto de avisos e erros detectados. O objetivo era recriar um arquivo conforme o usuário é editado em um documento, o que significa que haverá muitas solicitações de desfiapoção durante uma sessão do editor. Faz sentido manter um servidor em funcionamento para que um novo processo de refiapoção não precise ser iniciado para cada edição de usuário. Vários servidores de fiapos foram implementados, incluindo as extensões ESLint e TSLint do VS Code. Esses dois servidores com fiapos são implementados no TypeScript/JavaScript e executados em Node.js. Eles compartilham uma biblioteca que implementa a parte do cliente e do servidor do protocolo.

## <a name="how-the-lsp-works"></a>Como o LSP funciona

Um servidor de linguagem é executado em seu próprio processo e ferramentas como o Visual Studio ou VS Code se comunicam com o servidor usando o protocolo de linguagem sobre JSON-RPC. Outra vantagem do funcionamento do servidor de linguagem em um processo dedicado é que os problemas de desempenho relacionados a um único modelo de processo são evitados. O canal de transporte real pode ser stdio, soquetes, pipes nomeados ou IPC do nó se o cliente e o servidor forem gravados em Node.js.

Veja abaixo um exemplo de como uma ferramenta e um servidor de idioma se comunicam durante uma sessão de edição de rotina:

![diagrama de fluxo de LSP](media/lsp-flow-diagram.png)

* **O usuário abre um arquivo (chamado de documento) na ferramenta**: a ferramenta notifica o servidor de idiomas de que um documento está aberto (' TextDocument/didOpen '). De agora em diante, a verdade sobre o conteúdo do documento não está mais no sistema de arquivos, mas mantida pela ferramenta na memória.

* **O usuário faz edições**: a ferramenta notifica o servidor sobre a alteração do documento (' TextDocument/didChange ') e as informações semânticas do programa são atualizadas pelo servidor de idioma. Como isso acontece, o servidor de linguagem analisa essas informações e notifica a ferramenta com os erros e avisos detectados (' textDocument/publishDiagnostics ').

* **O usuário executa "ir para definição" em um símbolo no editor**: a ferramenta envia uma solicitação de "textDocument/definição" com dois parâmetros: (1) o URI do documento e (2) a posição do texto de onde a solicitação ir para definição foi iniciada para o servidor. O servidor responde com o URI do documento e a posição da definição do símbolo dentro do documento.

* **O usuário fecha o documento (arquivo)**: uma notificação ' TextDocument/didClose ' é enviada da ferramenta, informando ao servidor de idioma que o documento agora não está mais na memória e que o conteúdo atual agora está atualizado no sistema de arquivos.

Este exemplo ilustra como o protocolo se comunica com o servidor de idioma no nível de recursos do editor, como "ir para definição", "localizar todas as referências". Os tipos de dados usados pelo protocolo são ' tipos de dados ' do editor ou do IDE como o documento de texto aberto no momento e a posição do cursor. Os tipos de dados não estão no nível de um modelo de domínio de linguagem de programação que normalmente forneceria árvores de sintaxe abstrata e símbolos de compilador (por exemplo, tipos resolvidos, namespaces,...). Isso simplifica significativamente o protocolo.

Agora, vamos examinar a solicitação de ' textDocument/Definition ' em mais detalhes. Abaixo estão as cargas que vão entre a ferramenta de cliente e o servidor de idioma para a solicitação "ir para definição" em um documento C++.

Esta é a solicitação:

```json
{
    "jsonrpc": "2.0",
    "id" : 1,
    "method": "textDocument/definition",
    "params": {
        "textDocument": {
            "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/use.cpp"
        },
        "position": {
            "line": 3,
            "character": 12
        }
    }
}
```

Esta é a resposta:

```json
{
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
        "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/provide.cpp",
        "range": {
            "start": {
                "line": 0,
                "character": 4
            },
            "end": {
                "line": 0,
                "character": 11
            }
        }
    }
}
```

No Retrospect, descrever os tipos de dados no nível do editor em vez de no nível do modelo de linguagem de programação é um dos motivos para o sucesso do protocolo de servidor de linguagem. É muito mais simples padronizar um URI de documento de texto ou uma posição de cursor em comparação com a padronização de uma árvore de sintaxe abstrata e símbolos de compilador em diferentes linguagens de programação.

Quando um usuário está trabalhando com idiomas diferentes, VS Code normalmente inicia um servidor de idioma para cada linguagem de programação. O exemplo a seguir mostra uma sessão na qual o usuário trabalha em arquivos Java e SASS.

![Java e Sass](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>Funcionalidades

Nem todo servidor de linguagem pode dar suporte a todos os recursos definidos pelo protocolo. Portanto, o cliente e o servidor anunciam seu conjunto de recursos com suporte por meio de ' Capabilities '. Por exemplo, um servidor anuncia que ele pode manipular a solicitação ' textDocument/Definition ', mas pode não tratar a solicitação ' Workspace/Symbol '. Da mesma forma, os clientes podem anunciar que são capazes de fornecer notificações ' prestes a salvar ' antes de um documento ser salvo, para que um servidor possa computar edições textuais para formatar automaticamente o documento editado.

## <a name="integrating-a-language-server"></a>Integrando um servidor de linguagem

A integração real de um servidor de idioma em uma determinada ferramenta não é definida pelo protocolo de servidor de idioma e é deixada para os implementadores de ferramenta. Algumas ferramentas integram os servidores de idiomas genericamente por ter uma extensão que pode ser iniciada e se comunicar com qualquer tipo de servidor de linguagem. Outros, como VS Code, criam uma extensão personalizada por servidor de idioma, para que uma extensão ainda seja capaz de fornecer alguns recursos de linguagem personalizados.

Para simplificar a implementação de servidores de idiomas e clientes, há bibliotecas ou SDKs para as partes do cliente e do servidor. Essas bibliotecas são fornecidas para diferentes idiomas. Por exemplo, há um [módulo de NPM de cliente de linguagem](https://www.npmjs.com/package/vscode-languageclient) para facilitar a integração de um servidor de idioma em uma extensão de vs Code e outro [módulo NPM de servidor de linguagem](https://www.npmjs.com/package/vscode-languageserver) para gravar um servidor de idioma usando Node.js. Esta é a [lista](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations) atual de bibliotecas de suporte.

## <a name="using-the-language-server-protocol-in-visual-studio"></a>Usando o protocolo de servidor de linguagem no Visual Studio

* [Adicionando uma extensão de protocolo de servidor de linguagem](adding-an-lsp-extension.md) -saiba como integrar um servidor de linguagem ao Visual Studio.
