---
title: Visão geral do protocolo de servidor de linguagem | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ad0e802bd63a9d489a98eb9f216e6739e378d590
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894853"
---
# <a name="language-server-protocol"></a>Language Server Protocol

## <a name="what-is-the-language-server-protocol"></a>O que é o protocolo de idioma do servidor?

Suporte avançados recursos de edição, como preenchimentos automáticos de código de origem ou **ir para definição** para uma linguagem de programação em um editor ou IDE é tradicionalmente muito difícil e demorada. Normalmente, ele requer a criação de um modelo de domínio (um scanner, um analisador, um verificador de tipo, um construtor e muito mais) na linguagem de programação do editor ou IDE. Por exemplo, o plug-in Eclipse CDT, que fornece suporte para C/C++ no IDE do Eclipse é escrito em Java, pois o próprio IDE do Eclipse é escrito em Java. Seguindo essa abordagem, isso significaria que a implementação de um modelo de domínio do C/C++ no TypeScript para Visual Studio Code e um modelo de domínio separadas em c# para Visual Studio.

Criação de modelos de linguagem específica de domínio também é muito mais fácil se uma ferramenta de desenvolvimento pode reutilizar as bibliotecas existentes do idioma específico. No entanto, essas bibliotecas são normalmente implementadas na linguagem de programação em si (por exemplo, C/C++ domínio adequado modelos são implementados em C/C++). Integrar uma biblioteca de C/C++ em um editor escrito em TypeScript é tecnicamente possível, mas difícil de fazer.

### <a name="language-servers"></a>Servidores de idioma

Outra abordagem é executar a biblioteca em seu próprio processo e usar a comunicação entre processos para se comunicar com ele. As mensagens enviadas e para trás formam um protocolo. O protocolo de servidor de linguagem (LSP) é o produto de padronização as mensagens trocadas entre uma ferramenta de desenvolvimento e um processo de servidor de linguagem. Usando servidores de idioma ou demons não é uma ideia nova ou novel. Editores, como Vim e Emacs feito isso há algum tempo fornecer suporte de preenchimento automático semântica. O objetivo de LSP era simplificar esses tipos de integrações e fornecem uma estrutura úteis para expor os recursos de idioma para uma variedade de ferramentas.

Ter um protocolo comum permite a integração de recursos de linguagem de programação em uma ferramenta de desenvolvimento sem complicação reutilizando uma implementação existente do modelo de domínio do idioma. Um servidor back-end do idioma poderia ser escrito em PHP, Python ou Java e o LSP que permite que ele ser facilmente integrada a uma variedade de ferramentas. O protocolo funciona em um nível comum de abstração para que uma ferramenta pode oferecer serviços de linguagem avançados sem a necessidade de compreender totalmente as nuances específicas para o modelo de domínio subjacente.

## <a name="how-work-on-the-lsp-started"></a>Como funcionam em LSP iniciado

O LSP evoluiu ao longo do tempo e hoje, ele está na versão 3.0. Ele iniciado quando o conceito de um servidor de linguagem foi obtido por OmniSharp para fornecer recursos avançados de edição para c#. Inicialmente, o OmniSharp usado o protocolo HTTP com uma carga JSON e foi integrado ao vários editores incluindo [Visual Studio Code](https://code.visualstudio.com).

Ao mesmo tempo, a Microsoft começou a trabalhar em um servidor de linguagem do TypeScript, com a ideia de que dão suporte a TypeScript nos editores, como Emacs e Sublime Text. Nessa implementação, um editor se comunica por meio do stdin/stdout com o processo de servidor TypeScript e usa uma carga JSON inspirado pelo protocolo do depurador V8 para solicitações e respostas. O servidor de TypeScript foi integrado ao TypeScript Sublime plug-in e o VS Code para edição avançada de TypeScript.

Depois de ter integrado a dois servidores de idioma diferente, a equipe do VS Code começou a explorar um protocolo de servidor de linguagem comum para editores e IDEs. Um protocolo comum permite que um provedor de linguagem de programação criar um servidor único idioma que pode ser consumido pelos IDEs diferentes. Um consumidor de servidor de idioma só tem que implementar o lado do cliente do protocolo de uma vez. Isso resulta em uma situação de ganhos para o provedor de linguagem de programação e o consumidor de idioma.

O protocolo de idioma do servidor é iniciado com o protocolo usado pelo servidor do TypeScript, expandi-lo com mais recursos de linguagem inspirados a API da linguagem de código do VS. O protocolo é feito com o RPC de JSON para invocação remota devido à sua simplicidade e bibliotecas existentes.

Os VS um arquivo de código de equipe com protótipo os com a implementação de vários servidores de linguagem linter que responderem às solicitações de protocolo para efetuar lint (verificação) e retornam um conjunto de erros e avisos detectados. O objetivo era lint um arquivo como as edições do usuário em um documento, o que significa que haverá muitas solicitações de linting durante uma sessão do editor. Ele fez sentido manter um servidor de backup e em execução para que um novo processo de linting não precisa ser iniciado para cada edição do usuário. Vários servidores linter foram implementados, incluindo o VS Code ESLint e TSLint extensões. Esses dois servidores linter são implementados no TypeScript/JavaScript e executar em Node. js. Eles compartilham uma biblioteca que implementa a parte cliente e servidor do protocolo.

## <a name="how-the-lsp-works"></a>Como funciona o LSP

Um servidor de linguagem é executado em seu próprio processo e ferramentas como o Visual Studio ou o VS Code se comunicar com o servidor usando o protocolo de idioma sobre RPC de JSON. Outra vantagem do servidor de linguagem que operam em um processo dedicado é que os problemas de desempenho relacionados a um modelo de processo único são evitados. O canal de transporte real pode ser stdio, soquetes, pipes nomeados ou nó ipc se o cliente e o servidor são escritos em Node. js.

Abaixo está um exemplo de como uma ferramenta e um servidor de linguagem se comunicar durante uma rotina de sessão de edição:

![diagrama de fluxo de LSP](media/lsp-flow-diagram.png)

* **O usuário abre um arquivo (conhecido como um documento) na ferramenta**: A ferramenta notifica o servidor de linguagem que um documento está aberto (' textDocument/didOpen'). De agora em diante, a verdade sobre o conteúdo do documento não está mais no sistema de arquivos, mas mantido pela ferramenta na memória.

* **O usuário fizer edições**: A ferramenta notifica o servidor sobre a alteração do documento (' textDocument/didChange') e as informações semânticas do programa são atualizadas pelo servidor de linguagem. Quando isso acontece, o servidor de linguagem analisa essas informações e notifica a ferramenta com os erros detectados e os avisos (' textDocument/publishDiagnostics').

* **O usuário executa "Ir para definição" em um símbolo no editor de**: A ferramenta envia uma solicitação de ' textDocument/definição' com dois parâmetros: (1) o URI do documento e (2) a posição do texto a partir de onde a ir para a solicitação da definição foi iniciada no servidor. O servidor responde com o URI do documento e a posição da definição do símbolo dentro do documento.

* **O usuário fecha o documento (arquivo)**: é enviada uma notificação de ' textDocument/didClose' da ferramenta, informando o servidor de idioma que o documento está agora, não há mais na memória e que o conteúdo atual é agora atualizados no sistema de arquivos.

Este exemplo ilustra como o protocolo se comunica com o servidor de linguagem no nível de recursos do editor, como "Go to Definition", "Localizar todas as referências". Os tipos de dados usados pelo protocolo são editor ou IDE 'tipos de dados' como o documento de texto aberto no momento e a posição do cursor. Os tipos de dados não estão no nível de um modelo de domínio de programação linguagem que normalmente forneceria árvores de sintaxe abstrata e os símbolos do compilador (por exemplo, os tipos resolvidos, namespaces,...). Isso simplifica o protocolo significativamente.

Agora vamos examinar a solicitação de ' textDocument/definição' em mais detalhes. Abaixo estão as cargas que passam entre a ferramenta de cliente e o servidor de linguagem para a solicitação de "Ir para definição" em um documento de C++.

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

Em retrospecto, que descreve os tipos de dados no nível do editor, em vez de no nível do modelo de linguagem de programação é um dos motivos para o sucesso do protocolo de idioma do servidor. É muito mais simples padronizar um URI do documento de texto ou uma posição do cursor em comparação com a padronização um símbolos de compilador e de árvore de sintaxe abstrata entre linguagens de programação diferentes.

Quando um usuário estiver trabalhando com idiomas diferentes, o VS Code inicia normalmente um servidor de idioma para cada linguagem de programação. O exemplo a seguir mostra uma sessão em que o usuário trabalha nos arquivos Java e SASS.

![Java e sass](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>Capacidades

Nem todo servidor de idioma pode dar suporte a todos os recursos definidos pelo protocolo. Portanto, o cliente e servidor anuncia seu conjunto de recursos com suporte por meio do 'capabilities'. Por exemplo, um servidor anuncia que pode manipular a solicitação de ' textDocument/definição', mas ele não pode manipular a solicitação de 'espaço de trabalho/symbol'. Da mesma forma, os clientes podem anunciar que eles sejam capazes de fornecer ' prestes a salvar' notificações antes de um documento é salvo, para que um servidor pode calcular edições textuais para formatar automaticamente o documento editado.

## <a name="integrating-a-language-server"></a>Integração de um servidor de linguagem

A integração real de um servidor de idioma em uma determinada ferramenta não está definida pelo protocolo de servidor de linguagem e é deixada para implementações de ferramenta. Algumas ferramentas integram servidores idiomas genericamente fazendo com que uma extensão que pode começar e se comunicar com qualquer tipo de servidor de linguagem. Outros, como o VS Code, criam uma extensão personalizada por servidor de idioma, para que uma extensão ainda é capaz de fornecer alguns recursos de idioma personalizado.

Para simplificar a implementação de linguagem de servidores e clientes, há bibliotecas ou SDKs para as partes do cliente e servidor. Essas bibliotecas são fornecidas para idiomas diferentes. Por exemplo, há um [módulo de npm de cliente de linguagem](https://www.npmjs.com/package/vscode-languageclient) para facilitar a integração de um servidor de idioma em uma extensão do VS Code e outro [módulo de npm do idioma do server](https://www.npmjs.com/package/vscode-languageserver) para gravar um servidor de idioma usando o Node. js. Isso é o atual [lista](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations) das bibliotecas de suporte.

## <a name="using-the-language-server-protocol-in-visual-studio"></a>Usando o protocolo de servidor de linguagem no Visual Studio

* [Adicionando uma extensão do protocolo de idioma do servidor](adding-an-lsp-extension.md) -Saiba mais sobre como integrar um servidor de linguagem no Visual Studio.
