---
title: Modo tela inteira e espaço virtual
ms.date: 11/04/2016
ms.topic: how-to
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f8f86d635e1e57d82dd2d18084c91a9267f9a0b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284198"
---
# <a name="how-to-manage-editor-modes"></a>Como gerenciar modos do editor

Você pode exibir o editor de código do Visual Studio em vários modos de exibição.

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos neste artigo, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, por exemplo, para configurações **Gerais** ou do **Visual C++**, escolha **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, escolha **Redefinir todas as configurações**.

## <a name="enable-full-screen-mode"></a>Habilitar o modo de tela inteira

Você pode optar por ocultar todas as janelas de ferramentas e exibir apenas janelas de documentos habilitando o modo de **tela inteira** .

- Pressione **ALT** + **Shift** + **Enter** para entrar ou sair do modo de **tela inteira** .

     -- ou --

- Emita o comando `View.Fullscreen` na janela **Comando**.

## <a name="enable-virtual-space-mode"></a>Habilitar o modo de espaço virtual

No modo **Espaço virtual**, os espaços são inseridos no final de cada linha de código. Selecione essa opção para posicionar comentários em um ponto consistente ao lado do seu código.

1. Selecione **Opções** no menu **Ferramentas**.

2. Expanda a pasta **Editor de Texto** e escolha **Todas as Linguagens** para definir essa opção globalmente ou escolha uma pasta de idioma específico. Por exemplo, para ativar números de linha somente em Visual Basic, escolha o **Basic**  >  nó**Editor de texto** básico.

3. Selecione as opções **Gerais** e, em **Configurações**, selecione **Habilitar Espaço virtual**.

    > [!NOTE]
    > O **Espaço virtual** está habilitado no modo **Seleção de Coluna**. Quando o modo **Espaço virtual** não está habilitado, o ponto de inserção é movido do final de uma linha diretamente para o primeiro caractere da próxima.

## <a name="see-also"></a>Veja também

- [Personalizar layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md)
- [Fontes e cores, caixa de diálogo ambiente, opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)
