---
title: Personalizar menus e barras de ferramentas
description: Saiba como personalizar menus e barras de ferramentas do Visual Studio, além de aprender a personalizar todos os comandos incluídos nos menus e barras de ferramentas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.renametoolbar
- vs.customize.toolbars
- vs.buttoneditor
- vs.customize.commands
- vs.newtoolbar
helpviewer_keywords:
- captions, customizing toolbar
- custom toolbars [Visual Studio]
- command buttons, customizing toolbar
- labels, customizing toolbar
- images [Visual Studio], toolbar buttons
- buttons [Visual Studio], custom toolbars
- toolbars [Visual Studio], creating in the IDE
- icons [Visual Studio], customizing toolbar
- commands [Visual Studio], customizing environment
- customizing toolbars
- toolbars [Visual Studio], customizing
- toolbars [Visual Studio], customizing in the IDE
ms.assetid: b570ae2f-5302-45dc-9cc9-8d4d1ad50603
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e9111631014275da92da73966ba0310971dbf27f
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95597218"
---
# <a name="how-to-customize-menus-and-toolbars-in-visual-studio"></a>Como personalizar menus e barras de ferramentas no Visual Studio

Para personalizar o Visual Studio, além de adicionar e remover barras de ferramentas e menus na barra de menus, você também pode adicionar e remover comandos em qualquer barra de ferramentas ou menu.

> [!WARNING]
> Depois de personalizar uma barra de ferramentas ou um menu, verifique se a respectiva caixa de seleção permanece marcada na caixa de diálogo **Personalizar**. Caso contrário, as alterações não persistirão depois que você fechar e reabrir o Visual Studio.

## <a name="add-remove-or-move-a-menu-on-the-menu-bar"></a>Adicionar, remover ou mover um menu na barra de menus

1. Na barra de menus, escolha **ferramentas**  >  **Personalizar**.

     A caixa de diálogo **Personalizar** é aberta.

2. Na guia **Comandos**, deixe o botão de opção **Barra de menus** selecionado, deixe **Barra de Menus** selecionado na lista ao lado dessa opção e realize um dos seguintes conjuntos de etapas:

    - Para adicionar um menu, escolha o botão **Adicionar Novo Menu**, escolha o botão **Modificar Seleção** e nomeie o menu que você deseja adicionar.

        ![Personalizar a caixa de diálogo mostrando como adicionar um menu](../ide/media/addmenu.png)

    - Para remover um menu, selecione-o na lista **Controles** e escolha o botão **Excluir**.

    - Para mover um menu na barra de menus, escolha o menu na lista **Controles** e escolha o botão **Mover para Cima** ou **Mover para Baixo**.

## <a name="add-remove-or-move-a-toolbar"></a>Adicionar, remover ou mover uma barra de ferramentas

1. Na barra de menus, escolha **ferramentas**  >  **Personalizar**.

     A caixa de diálogo **Personalizar** é aberta.

2. Na guia **Barra de Ferramentas**, realize um dos seguintes conjuntos de etapas:

    - Para adicionar uma barra de ferramentas, escolha o botão **Novo**, especifique um nome para a barra de ferramentas que você deseja adicionar e escolha o botão **OK**.

        ![Personalizar a caixa de diálogo mostrando como adicionar uma barra de ferramentas](../ide/media/addtoolbar.png)

    - Para remover uma barra de ferramentas personalizada, selecione-a na lista **Barras de Ferramentas** e escolha o botão **Excluir**.

        > [!IMPORTANT]
        > Você pode excluir as barras de ferramentas que cria, mas não as barras de ferramentas padrão.

    - Para mover uma barra de ferramentas para outro local de encaixe, selecione-a na lista **Barras de Ferramentas**, escolha o botão **Modificar Seleção** e escolha um local na lista exibida.

        Você também pode arrastar uma barra de ferramentas pela sua borda esquerda para movê-la para qualquer lugar na área de encaixe principal.

        > [!NOTE]
        > Para obter mais informações sobre como melhorar a usabilidade e a acessibilidade das barras de ferramentas, consulte [Como definir opções de acessibilidade do IDE](../ide/reference/how-to-set-ide-accessibility-options.md).

## <a name=""></a><a name="customizing_menu">Personalizar um menu ou uma barra de ferramentas</a>

1. Na barra de menus, escolha **ferramentas**  >  **Personalizar**.

    A caixa de diálogo **Personalizar** é aberta.

2. Na guia **Comandos**, escolha o botão de opção do tipo de elemento que você deseja personalizar.

3. Na lista desse tipo de elemento, escolha o menu ou a barra de ferramentas que deseja personalizar e executa um dos seguintes conjuntos de etapas:

    - Para adicionar um comando, escolha o botão **Adicionar Comando**.

        Na caixa de diálogo **Adicionar Comando**, escolha um item na lista **Categorias**, escolha um item na lista **Comandos** e escolha o botão **OK**.

        ![Adicionar caixa de diálogo Comando no Visual Studio](../ide/media/addcommand.png)

    - Para excluir um comando, escolha-o na lista **Controles** e escolha o botão **Excluir**.

    - Para reorganizar comandos, escolha um comando na lista **Controles** e escolha o botão **Mover para Cima** ou **Mover para Baixo**.

    - Para agrupar comandos em uma linha horizontal, primeiro escolha um comando na lista **Controles**, escolha o botão **Modificar Seleção** e, em seguida, escolha **Começar um Grupo** no menu exibido.

## <a name="reset-a-menu-or-a-toolbar"></a>Redefinir um menu ou uma barra de ferramentas

1. Na barra de menus, escolha **ferramentas**  >  **Personalizar**.

    A caixa de diálogo **Personalizar** é aberta.

2. Na guia **Comandos**, escolha o botão de opção do tipo de elemento que você deseja redefinir.

3. Na lista desse tipo de elemento, escolha o menu ou a barra de ferramentas que deseja redefinir.

4. Escolha o botão **Modificar Seleção** e escolha **Redefinir** no menu exibido.

    Também é possível redefinir todos os menus e barras de ferramentas escolhendo o botão **Redefinir Tudo**.

## <a name="see-also"></a>Confira também

- [Personalizar o IDE](../ide/personalizing-the-visual-studio-ide.md)
- [Personalizar o editor](../ide/how-to-change-text-case-in-the-editor.md)
