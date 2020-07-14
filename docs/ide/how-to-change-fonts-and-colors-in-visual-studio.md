---
title: Alterar fontes e cores
ms.date: 06/01/2020
ms.topic: how-to
helpviewer_keywords:
- Visual Studio, color themes
- color themes, Visual Studio
ms.assetid: 60d91ba1-244b-4c43-847f-60b744f1352a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0eb2373117b382cb19f374581ada45a5732b9c4c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284666"
---
# <a name="how-to-change-fonts-and-colors-in-visual-studio"></a>Como alterar fontes e cores no Visual Studio

Você pode alterar as fontes e as cores no Visual Studio de várias maneiras. Por exemplo, você pode alterar o tema de cor azul padrão para o tema escuro (também conhecido como "modo escuro".) E você pode alterar a fonte padrão e o tamanho do texto para uma fonte e um tamanho diferentes.

## <a name="change-the-color-theme"></a>Alterar o tema de cores

Veja como alterar o tema de cores do quadro do IDE e as janelas de ferramentas no Visual Studio.

1. Na barra de menus, escolha **ferramentas**  >  **Opções**.

1. Na lista de opções, escolha **ambiente**  >  **geral**.

1. Na lista **tema de cores** , escolha o tema **azul** padrão, o tema **claro** , o tema **escuro** ou o tema **azul (contraste adicional)** .

   ![Captura de tela da caixa de diálogo opções para alterar o tema de cores](media/fonts-colors-theme.png "Captura de tela da caixa de diálogo opções que você pode usar para alterar o tema de cores")

    > [!NOTE]
    > Quando você altera um tema de cor, o texto no IDE reverte para as fontes e tamanhos padrão ou anteriormente personalizados para esse tema.

    :::moniker range="vs-2017"

    > [!TIP]
    > Você pode criar e editar seus próprios temas do Visual Studio instalando o [Editor de tema de cores para o visual studio 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor).

    :::moniker-end

    :::moniker range="vs-2019"

    > [!TIP]
    > Você pode criar e editar seus próprios temas do Visual Studio instalando o [Designer de tema de cores do Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner).

    :::moniker-end

## <a name="change-fonts-and-text-size"></a>Alterar fontes e tamanho do texto

Você pode alterar a fonte e o tamanho do texto para todas as janelas de ferramentas e quadros IDE, ou apenas para determinados elementos de texto ou do Windows. Também é possível alterar a fonte e o tamanho do texto no editor.

### <a name="to-change-the-font-and-text-size-in-the-ide"></a>Para alterar a fonte e o tamanho do texto no IDE

1. Na barra de menus, escolha **ferramentas**  >  **Opções**.

1. Na lista opções, escolha **Environment**  >  **fontes e cores**do ambiente.

1. Na lista **Mostrar configurações de** , escolha **ambiente**.

   ![Captura de tela da caixa de diálogo opções para alterar as fontes e cores no IDE](media/fonts-colors-environment.png "Captura de tela da caixa de diálogo opções para alterar as fontes e cores no IDE")

    > [!NOTE]
    > Se você desejar alterar apenas a fonte das janelas de ferramentas, na lista **Mostrar configurações de**, escolha **Todas as janelas de ferramentas de texto**.

1. Modifique as opções de **fonte** e **tamanho** para alterar a fonte e o tamanho do texto do IDE.

1. Selecione o item apropriado em **Exibir itens** e, em seguida, modifique as opções **Primeiro plano do item** e **Tela de fundo do item**.

### <a name="to-change-the-font-and-text-size-in-the-editor"></a>Para alterar a fonte e o tamanho do texto no editor

1. Na barra de menus, escolha **ferramentas**  >  **Opções**.

1. Na lista opções, escolha **Environment**  >  **fontes e cores**do ambiente.

1. Na lista **Mostrar configurações de** , selecione **Editor de texto**.

   ![Captura de tela da caixa de diálogo opções para alterar as fontes e cores no editor](media/fonts-colors-text-editor.png "Captura de tela da caixa de diálogo opções para alterar as fontes e cores no editor")

1. Modifique as opções de **fonte** e **tamanho** para alterar a fonte e o tamanho do texto do editor.

1. Selecione o item apropriado em **Exibir itens** e, em seguida, modifique as opções **Primeiro plano do item** e **Tela de fundo do item**.

Para obter mais informações, consulte a página [alterar fontes e cores para o editor](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md) .

## <a name="accessibility-options"></a>Opções de acessibilidade

Há opções de tema de cores para você se tiver uma visão baixa. Você pode usar uma opção de alto contraste para *todos* os aplicativos e a interface do usuário em um computador ou uma opção de contraste adicional somente para o Visual Studio.

### <a name="use-windows-high-contrast"></a>Usar alto contraste do Windows

Use qualquer um dos procedimentos a seguir para alternar a opção de alto contraste do Windows:

- No Windows ou em qualquer aplicativo da Microsoft, pressione a tecla **ALT**esquerda + **Shift** + **PrtScn** teclas.

- No Windows, escolha **Iniciar**  >  **configurações**  >  **facilidade de acesso de**  >  **alto contraste**.

    > [!WARNING]
    > A configuração de alto contraste do Windows afeta todos os aplicativos e a interface do usuário no computador.

### <a name="use-visual-studio-extra-contrast"></a>Usar o Visual Studio contraste extra

Use os procedimentos a seguir para alternar a opção de contraste extra do Visual Studio:

1. Na barra de menus no Visual Studio, escolha **ferramentas**  >  **Opções**e, em seguida, na lista opções, escolha **ambiente**  >  **geral**.

1. Na lista suspensa **tema de cores** , escolha o tema **azul (contraste adicional)** e escolha **OK**.

Para saber mais sobre outras opções de acessibilidade do Visual Studio disponíveis, consulte a página [recursos de acessibilidade do Visual Studio](../ide/reference/accessibility-features-of-visual-studio.md) .

> [!TIP]
> Se houver uma opção de acessibilidade para cores ou fontes que você ache que pode ser útil, mas que não está disponível atualmente no Visual Studio, informe-nos selecionando **sugerir um recurso** na [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/). Para obter mais informações sobre esse fórum e como ele funciona, consulte a página [sugerir um recurso](../ide/suggest-a-feature.md) .

## <a name="next-steps"></a>Próximas etapas

Para saber mais detalhes sobre todos os elementos da interface do usuário para os quais você pode alterar os esquemas de fontes e cores, consulte a página da [caixa de diálogo fontes e cores, ambiente, opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md) .

## <a name="see-also"></a>Veja também

- [Alterar fontes e cores para o editor de códigos](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md)
- [Recursos do editor de código do Visual Studio](../ide/writing-code-in-the-code-and-text-editor.md)