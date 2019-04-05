---
title: Começando a desenvolver extensões | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 03c9ebb2a2c84c400b4fb2d3aea4c3ec121fbf27
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "59000070"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Começando a desenvolver extensões do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você nunca escreveu uma extensão do Visual Studio antes, você provavelmente terá algumas perguntas. Apresentaremos alguns dos mais comuns aqui. Se você não vir as informações que você está procurando, use os botões de comentários (**esta página foi útil?** na parte inferior da tela) para fazer o que você deseja.

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>Qual software precisa desenvolver extensões do Visual Studio?
 Você precisará instalar o SDK do Visual Studio 2015, além do Visual Studio 2015 para desenvolver extensões do Visual Studio.   Você pode instalar o SDK do Visual Studio 2015 como parte da instalação regular, ou você pode instalá-lo mais tarde. Para obter mais informações sobre como instalar o SDK do Visual Studio, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Quais tipos de coisas que pode fazer com as extensões do Visual Studio?
 O céu 's o limite quando se trata de imaginando diferentes extensões do Visual Studio. Obviamente, a maioria das extensões ter algo a ver com a escrita de código, mas que não precisa ser o caso. Aqui estão alguns exemplos dos tipos de extensões, que você pode criar:

- Suporte para idiomas que não estão incluídos no Visual Studio, com a coloração de sintaxe, IntelliSense e suporte de compilador e depuração

- Ferramentas de produtividade que ampliam o núcleo do IDE experiência com modelos adicionais, caixas de diálogo Novo, refatoração de código ou janelas de ferramentas

- Designers específicos de domínio para cenários como o suporte de design ou na nuvem de dados

  Para obter exemplos de extensões, confira a [Visual Studio Marketplace](https://marketplace.visualstudio.com/). Você também pode dar uma olhada [extensões do código-fonte Visual Studio abra](https://github.com/Microsoft/extendvs/blob/master/CommunityExtensions.md).

## <a name="which-visual-studio-features-can-i-extend"></a>Quais recursos do Visual Studio pode estender?
 Em teoria, você pode estender qualquer parte do Visual Studio: menus, barras de ferramentas, comandos, windows, soluções, projetos, editores e assim por diante.

 Na prática, descobrimos que os recursos que a maioria das pessoas que desejam estender são comandos, menus e barras de ferramentas, windows, IntelliSense e projetos. Aqui estão links para as seções relevantes:

-   [Estendendo os Menus e comandos](../extensibility/extending-menus-and-commands.md): adicionar seus próprios itens de menus do Visual Studio e barras de ferramentas. Você pode usá-los para iniciar a nova funcionalidade do Visual Studio ou seus próprios aplicativos de ajuda externo. Você também pode fornecer atalhos personalizados para seus itens de menu.

-   [Estendendo e personalizando ferramenta Windows](../extensibility/extending-and-customizing-tool-windows.md): estender as janelas de ferramentas existente ou criar suas próprias janelas de ferramenta. Por exemplo, você pode adicionar novas propriedades para o **propriedades**, ou você poderia criar uma nova janela de ferramenta para adicionar recursos adicionais.

-   [Editor e extensões do serviço de linguagem](../extensibility/editor-and-language-service-extensions.md): adicionar suas próprias personalizações, o IntelliSense fornecido para linguagens do Visual Studio ou criar suporte para novas linguagens de programação. Você pode criar novos conclusões de instruções, sugestões e dicas de ferramenta de QuickInfo novo. Com lâmpadas, você pode adicionar sugestões de refatoração e correções de código para dar suporte a novas linguagens de programação.

-   [Estender projetos](../extensibility/extending-projects.md)

-   [Estender opções e configurações de usuário](../extensibility/extending-user-settings-and-options.md)

-   [Estender propriedades e a janela de propriedades](../extensibility/extending-properties-and-the-property-window.md)

-   [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)

-   [Shell isolado do Visual Studio](../extensibility/visual-studio-isolated-shell.md)

##  <a name="BKMK_ProjectTemplate"></a> Quais modelos de projeto são fornecidos pelo VSSDK?
 Os dois tipos principais de extensões são extensões VSPackages e MEF. Em geral, as extensões VSPackage são usadas para extensões que usam ou estendem comandos, janelas de ferramentas e projetos. Extensões do MEF são usadas para estender ou personalizar o editor do Visual Studio.

 Extensões do Visual c# e Visual Basic, VSSDK fornece um modelo de projeto VSIX vazio que pode ser usado junto com os novos modelos de item que criar comandos de menu, janelas de ferramentas e extensões do editor. Para obter mais informações, consulte [o que há de novo no SDK do Visual Studio 2015](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md). Você também pode usar este modelo para modelos de projeto de pacote, trechos de código e outros artefatos para distribuição a outros usuários.

 Para C++, o Assistente de VSPackage fornece o código para adicionar comandos de menu, janelas de ferramentas e editores personalizados.

 O modelo de Shell isolado é usado para empacotar uma extensão em uma versão do shell do Visual Studio que você pode definir a marca e distribuir como seu próprio. Os tópicos a seguir mostram como começar a usar com cada tipo de extensão:

-   Comandos de menu: [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

-   Janelas de ferramentas: [Criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md)

-   Extensões do Editor: [Criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md)

-   VSPackages básicos: [Criar uma extensão com um VSPackage](../extensibility/creating-an-extension-with-a-vspackage.md)

-   Modelo de projeto do VSIX: [Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)

-   Shell isolado do Visual Studio: [Passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>Como obtenho minha extensão para se parecer com o Visual Studio?
 Obtenha ótimas dicas para projetar a interface do usuário para a sua extensão em [diretrizes de experiência de usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).

## <a name="where-can-i-find-examples-of-vssdk-code"></a>Onde posso encontrar exemplos de código VSSDK?
 Cada um dos links listados na seção anterior ter orientações passo a passo que mostram como implementar recursos específicos. Você também pode encontrar código-fonte aberto exemplos de VSSDK no GitHub em [exemplos do Visual Studio](https://aka.ms/vs2015sdksamples).

## <a name="how-can-i-distribute-my-extension"></a>Como distribuir o minha extensão?
 Você pode instalar sua extensão em outro computador ou enviá-lo para seus amigos como um arquivo. VSIX, que podem ser instalado clicando duas vezes nele. Você pode encontrar mais informações sobre pacotes VSIX [envio extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).

 Você também pode publicar sua extensão na Galeria do Visual Studio, que se torna visível para um grande número de clientes do Visual Studio. Para obter um exemplo de empacotamento de uma extensão da galeria, consulte [passo a passo: Publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md). Para obter mais informações sobre o que você precisa fazer para publicar na galeria, consulte [produtos e extensões do Visual Studio](https://visualstudiogallery.msdn.microsoft.com/).
