---
title: Modo tela inteira e espaço virtual do Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- views, virtual space
- line numbers, displaying
- virtual space mode
- line numbers
- Code Editor, view and display options
- full screen mode
- Code Editor, modes
- views, splitting
- views, word wrapping
- fonts and size
- views, creating new windows
- views, line numbers
- views, changing mode
- views, outlining
ms.assetid: 1fb48027-d870-439f-8b72-4a0321390748
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 94bc99bf70340ef76639d0ae0f05e1f7737173a2
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31943342"
---
# <a name="how-to-manage-editor-modes"></a>Como gerenciar modos do editor

Você pode exibir o editor de código do Visual Studio em vários modos de exibição.

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos neste artigo, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, por exemplo, para configurações **Gerais** ou do **Visual C++**, escolha **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, escolha **Redefinir todas as configurações**.

## <a name="enable-full-screen-mode"></a>Habilitar o modo de tela inteira

É possível escolher ocultar todas as janelas de ferramentas e exibir apenas janelas do documento, habilitando o modo de **Tela Inteira**.

-   Pressione **ALT**+**SHIFT**+**ENTER** para entrar ou sair do modo de **Tela Inteira**.

     --ou--

-   Emita o comando `View.Fullscreen` na janela **Comando**.

## <a name="enable-virtual-space-mode"></a>Habilitar o modo de espaço virtual

No modo **Espaço virtual**, os espaços são inseridos no final de cada linha de código. Selecione essa opção para posicionar comentários em um ponto consistente ao lado do seu código.

1.  Selecione **Opções** no menu **Ferramentas**.

2.  Expanda a pasta **Editor de Texto** e escolha **Todas as Linguagens** para definir essa opção globalmente ou escolha uma pasta de idioma específico. Por exemplo, para ativar os números de linha apenas no Visual Basic, escolha o nó **Básico** > **Editor de Texto**.

3.  Selecione as opções **Gerais** e, em **Configurações**, selecione **Habilitar Espaço virtual**.

    > [!NOTE]
    > O **Espaço virtual** está habilitado no modo **Seleção de Coluna**. Quando o modo **Espaço virtual** não está habilitado, o ponto de inserção é movido do final de uma linha diretamente para o primeiro caractere da próxima.

## <a name="see-also"></a>Consulte também

- [Personalizar o editor](../ide/customizing-the-editor.md)
- [Personalizar layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md)
- [Caixa de diálogo Fontes e Cores, Ambiente, Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)