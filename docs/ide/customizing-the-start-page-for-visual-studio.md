---
title: Instalar uma página inicial personalizada ou alterar o item de inicialização no Visual Studio
ms.date: 02/01/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.ToolsOptionsPages.Startup
helpviewer_keywords:
- Start Page [Visual Studio]
- customizing Start Page [Visual Studio]
- Visual Studio Start Page
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b5e32a311bcd60542df80518c791b1fbe413a7b2
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31916601"
---
# <a name="customize-the-start-page-for-visual-studio"></a>Personalizar a página inicial do Visual Studio

É possível personalizar a experiência de inicialização do Visual Studio de várias maneiras diferentes, mostrando, por exemplo, a caixa de diálogo **Abrir Projeto** ou abrindo a solução que foi carregada mais recentemente. Também é possível mostrar uma página inicial personalizada, que é uma página XAML do Windows Presentation Foundation (WPF) executada em uma janela de ferramenta e pode executar comandos que são internos do Visual Studio.

## <a name="to-change-the-startup-item"></a>Para alterar o item de inicialização

1. Na barra de menus, escolha **Ferramentas** > **Opções**.

1. Expanda **Ambiente** e escolha **Inicialização**.

1. Na lista **Na inicialização**, escolha o item a ser exibido depois que o Visual Studio inicia.

## <a name="to-show-a-custom-start-page"></a>Para mostrar uma página inicial personalizada

Você pode [criar sua própria página inicial personalizada](../extensibility/creating-a-custom-start-page.md) usando o SDK do Visual Studio ou usar uma que alguém criou. Por exemplo, você pode encontrar as páginas iniciais personalizadas no [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=Start%20Pages&sortBy=Downloads).

Para instalar uma página inicial personalizada, abra um arquivo *.vsix* ou copie e cole os arquivos de página inicial na pasta *%USERPROFILE% \Documents\Visual Studio 2017\StartPages* do computador.

### <a name="to-select-which-custom-start-page-to-display"></a>Para selecionar qual página inicial personalizada exibir

1. Na barra de menus, escolha **Ferramentas** > **Opções**.

1. Expanda **Ambiente** e escolha **Inicialização**.

1. Na lista **Personalizar Página Inicial**, escolha a página desejada.

> [!NOTE]
> Se um erro em uma página inicial personalizada causar pane no Visual Studio, você poderá iniciar o Visual Studio no modo de segurança e defini-lo para usar a página inicial padrão. Consulte [/SafeMode (devenv.exe)](../ide/reference/safemode-devenv-exe.md).

## <a name="see-also"></a>Consulte também

- [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md)