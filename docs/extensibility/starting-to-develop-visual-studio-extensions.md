---
title: Começando a desenvolver extensões do Visual Studio | Microsoft Docs
ms.date: 09/18/2017
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8745acd9af9009a7206eada7ffb64f95759e8399
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286187"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Começar a desenvolver extensões do Visual Studio

Se você nunca escreveu uma extensão do Visual Studio antes, provavelmente terá algumas dúvidas. Listamos alguns dos mais comuns aqui. Se você não vir as informações que está procurando, use os botões de comentários (**essa página é útil?** no canto superior direito da tela) para solicitar o que você deseja.

> [!NOTE]
> Este artigo se aplica ao Visual Studio no Windows. Para Visual Studio para Mac, consulte [Estendendo Visual Studio para Mac](/visualstudio/mac/extending-visual-studio-mac). Para Visual Studio Code, consulte [API de extensão de Visual Studio Code](https://code.visualstudio.com/api).

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>De qual software eu preciso para desenvolver extensões do Visual Studio?

Você precisa instalar o SDK do Visual Studio, além do Visual Studio, para desenvolver extensões do Visual Studio. Você pode instalar o SDK do Visual Studio como parte da configuração normal ou pode instalá-lo mais tarde. Para obter mais informações sobre como instalar o SDK do Visual Studio, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Que tipos de coisas posso fazer com as extensões do Visual Studio?

O céu é o limite quando se trata de imaginar diferentes extensões do Visual Studio. É claro que a maioria das extensões tem algo a ver com a escrita de código, mas isso não precisa ser o caso. Aqui estão alguns exemplos dos tipos de extensões que você pode criar:

- Suporte para idiomas que não estão incluídos no Visual Studio, com codificação de cores de sintaxe, IntelliSense e compilador e suporte de depuração

- Ferramentas de produtividade que estendem a experiência principal do IDE com modelos adicionais, refatoração de código, novas caixas de diálogo ou janelas de ferramentas

- Designers específicos de domínio para cenários como design de dados ou suporte de nuvem

Para obter exemplos de extensões, confira o [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs). Muitas extensões são de software livre e o Marketplace inclui links para seu repositório GitHub.

## <a name="which-visual-studio-features-can-i-extend"></a>Quais recursos do Visual Studio posso estender?

Teoricamente, você pode estender praticamente qualquer parte do Visual Studio: menus, barras de ferramentas, comandos, janelas, soluções, projetos, editores e assim por diante.

Na prática, descobrimos que os recursos que a maioria das pessoas desejam estender são comandos, menus e barras de ferramentas, Windows, IntelliSense e projetos. Aqui estão os links para as seções relevantes:

- [Estendendo menus e comandos](../extensibility/extending-menus-and-commands.md): Adicione seus próprios itens aos menus e às barras de ferramentas do Visual Studio. Você pode usá-los para iniciar a nova funcionalidade do Visual Studio ou seus próprios aplicativos auxiliares externos. Você também pode fornecer atalhos personalizados para seus itens de menu.

- [Estendendo e personalizando janelas de ferramentas](../extensibility/extending-and-customizing-tool-windows.md): estenda as janelas de ferramentas existentes ou crie suas próprias janelas de ferramentas. Por exemplo, você pode adicionar novas propriedades às **Propriedades**ou criar uma nova janela de ferramenta para adicionar recursos adicionais.

- [Extensões de serviço de editor e de linguagem](../extensibility/editor-and-language-service-extensions.md): Adicione suas próprias personalizações ao IntelliSense fornecido para as linguagens do Visual Studio ou crie suporte para novas linguagens de programação. Você pode criar novas instruções de instrução, sugestões e novas dicas de ferramenta QuickInfo. Com lâmpadas leves, você pode adicionar sugestões de refatoração e correções de código para dar suporte a novas linguagens de programação.

- [Estender projetos](../extensibility/extending-projects.md)

- [Estender opções e configurações de usuário](../extensibility/extending-user-settings-and-options.md)

- [Estender propriedades e a janela de propriedades](../extensibility/extending-properties-and-the-property-window.md)

- [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)

- [Shell isolado do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a>Quais modelos de projeto são fornecidos pelo VSSDK?
 Os dois tipos principais de extensões são VSPackages e extensões de MEF. Em geral, as extensões VSPackage são usadas para extensões que usam ou estendem comandos, janelas de ferramentas e projetos. As extensões do MEF são usadas para estender ou personalizar o editor do Visual Studio.

 Para as extensões Visual C# e Visual Basic, o VSSDK fornece um modelo de projeto VSIX vazio que você pode usar junto com os novos modelos de item que criam comandos de menu, janelas de ferramentas e extensões do editor. Você também pode usar esse modelo para empacotar modelos de projeto, trechos de código e outros artefatos para distribuição para outros usuários.

 Para o C++, o assistente de VSPackage fornece o código para adicionar comandos de menu, janelas de ferramentas e editores personalizados.

 O modelo de shell isolado é usado para empacotar uma extensão em uma versão do shell do Visual Studio que você pode marcar e distribuir como o seu próprio. Os tópicos a seguir mostram como começar a usar cada tipo de extensão:

- Comandos de menu: [criando uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

- Janelas de ferramentas: [criando uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md)

- Extensões do editor: [criando uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- VSPackages básico: [criando uma extensão com um VSPackage](../extensibility/creating-an-extension-with-a-vspackage.md)

- Modelo de projeto VSIX: [introdução com o modelo de projeto VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>Como fazer obter minha extensão para se parecer com o Visual Studio?
 Obtenha ótimas dicas para criar a interface do usuário para sua extensão nas [diretrizes de experiência do usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).

## <a name="where-can-i-find-examples-of-vssdk-code"></a>Onde posso encontrar exemplos de código VSSDK?
 Cada um dos links listados na seção anterior apresenta orientações passo a passo que mostram como implementar recursos específicos. Você também pode encontrar exemplos de VSSDK de código-fonte aberto no GitHub em [exemplos do Visual Studio](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

## <a name="how-can-i-distribute-my-extension"></a>Como posso distribuir minha extensão?
 Você pode instalar sua extensão em outro computador ou enviá-la para seus amigos como um arquivo. vsix, que você instala clicando duas vezes nele. Você pode saber mais sobre os pacotes VSIX no [envio de extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).

 Você também pode publicar sua extensão na Visual Studio Marketplace, o que a torna visível para um grande número de clientes do Visual Studio. Para obter um exemplo de empacotamento de uma extensão para o Marketplace, consulte [passo a passos: publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md). Para obter mais informações sobre o que você precisa fazer para publicar no Marketplace, consulte [produtos e extensões do Visual Studio](/azure/devops/extend/overview?view=vsts).

## <a name="see-also"></a>Veja também

- [Estendendo o Visual Studio para Mac](/visualstudio/mac/extending-visual-studio-mac)
- [Estendendo Visual Studio Code](https://code.visualstudio.com/api)
