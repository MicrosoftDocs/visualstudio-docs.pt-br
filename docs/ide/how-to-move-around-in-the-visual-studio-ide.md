---
title: Como mover-se no IDE
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- environments [Visual Studio], navigation
- documents [Visual Studio], navigating
- IDE, navigation
- navigation [Visual Studio]
- files [Visual Studio], navigating between
- windows [Visual Studio], navigating
- Window.NextDocumentWindowNav
- IDE navigator
ms.assetid: 6c36b6eb-c93f-496b-af08-4199f7afd8bd
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f48ecaa6baf60cc62d51bd2548a16e62d8aac3e
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54985819"
---
# <a name="how-to-move-around-in-the-visual-studio-ide"></a>Como: Mover-se no IDE do Visual Studio

O IDE (ambiente de desenvolvimento integrado) foi projetado para que você possa mover de uma janela para outra e de um arquivo para outro de várias maneiras diferentes, dependendo dos requisitos do projeto ou de preferência. Você pode optar por percorrer os arquivos abertos no editor ou percorrer todas as janelas de ferramentas ativas no IDE. Você também pode mudar diretamente para qualquer arquivo aberto no editor, independentemente da ordem em que ele foi acessado pela última vez. Esses recursos podem ajudar a aumentar sua produtividade ao trabalhar no IDE.

> [!NOTE]
> As opções disponíveis nas caixas de diálogo e os nomes os locais dos comandos de menu que você vê podem diferir do que é descrito neste artigo, dependendo de suas configurações ativas ou da edição. Este artigo foi escrito considerando configurações **Gerais**. Para alterar as configurações, por exemplo, para configurações **Gerais** ou do **Visual C++**, escolha **Ferramentas** > **Importar e Exportar Configurações** e, em seguida, escolha **Redefinir todas as configurações**.

## <a name="keyboard-shortcuts"></a>Atalhos de teclado

Quase todos os comandos de menu no Visual Studio têm um atalho de teclado. Também é possível criar seus próprios atalhos personalizados. Para obter mais informações, consulte [Identificar e personalizar atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).

## <a name="navigate-among-files-in-the-editor"></a>Navegar entre arquivos no editor

Você pode usar vários métodos para percorrer os arquivos abertos no editor. Você pode percorrer os arquivos com base na ordem em que os acessa, usar o Navegador de IDE para localizar rapidamente qualquer arquivo aberto no momento ou fixar arquivos favoritos à guia também para que fiquem sempre visíveis.

Navegar para Trás e Navegar para Frente percorre os arquivos abertos no editor baseado na ordem em que foram acessados, de modo muito semelhante a Voltar e Avançar no histórico de exibição no Microsoft Internet Explorer.

### <a name="to-move-through-open-files-in-order-of-use"></a>Para percorrer os arquivos abertos por ordem de uso

-   Para ativar os documentos abertos na ordem em que foram utilizados mais recentemente, pressione **CTRL**+**-**.

-   Para ativar os documentos abertos na ordem inversa, pressione **CTRL**+**SHIFT**+**-**.

    > [!NOTE]
    > As opções **Navegar para Trás** e **Navegar para Frente** também podem ser encontradas no menu **Exibir**.

Você também pode mudar para um arquivo específico aberto no editor, independentemente de quando o arquivo foi acessado pela última vez, usando o **Navegador de IDE**, a lista **Arquivos Ativos** no editor ou a caixa de diálogo **Windows**.

O **Navegador de IDE** funciona de modo muito semelhante ao gerenciador de aplicativos do Windows. Ele não está disponível nos menus e pode ser acessado somente usando teclas de atalho. Você pode usar qualquer um dos dois comandos para acessar o **Navegador de IDE** (mostrado abaixo) para percorrer os arquivos, dependendo da ordem na qual deseja percorrê-los.

![Navegador na IDE do Visual Studio](../ide/media/vs2015_ide_navigator.png)

O `Window.PreviousDocumentWindowNav` permite ir para o arquivo acessado mais recentemente e `Window.NextDocumentWindowNav` permite mover-se na ordem inversa. As **Configurações Gerais de Desenvolvimento** atribuem **Shift**+**Alt**+**F7** a `Window.PreviousDocumentWindowNav` e **Alt**+**F7** a `Window.NextDocumentWindowNav`.

> [!NOTE]
> Se a combinação de configurações que você está usando ainda não tiver uma combinação de teclas de atalho atribuída a esse comando, você poderá atribuir seu próprio comando personalizado usando a página **Teclado** da caixa de diálogo **Opções**. Para obter mais informações, consulte [Identificar e personalizar atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).

### <a name="to-switch-to-specific-files-in-the-editor"></a>Para mudar para arquivos específicos no editor

-   Pressione **CTRL**+**TAB** para exibir o **Navegador de IDE**. Mantenha pressionada a tecla **Ctrl** e pressione **Tab** repetidamente até selecionar o arquivo para o qual você deseja mudar.

    > [!TIP]
    > Para inverter a ordem em que você percorre a lista **Arquivos Ativos**, mantenha pressionadas as teclas **CTRL**+**SHIFT** e pressione a tecla **TAB**.

    \- ou -

-   No canto superior direito do editor, escolha o botão **Arquivos Ativos** e, em seguida, selecione um arquivo na lista para mudar para ele.

    \- ou -

-   Na barra de menus, escolha **Janela** > **Janelas**.

-   Na lista, selecione o arquivo que você deseja exibir e, em seguida, escolha **Ativar**.

## <a name="navigate-among-tool-windows-in-the-ide"></a>Navegar entre janelas de ferramentas no IDE

O **Navegador de IDE** também permite percorrer as janelas de ferramenta abertas no IDE. Você pode usar qualquer um dos dois comandos para acessar o **Navegador de IDE** para percorrer janelas de ferramentas, dependendo da ordem na qual deseja percorrê-las. O `Window.PreviousToolWindowNav` permite ir para o arquivo acessado mais recentemente e `Window.NextToolWindowNav` permite mover-se na ordem inversa. As **Configurações Gerais de Desenvolvimento** atribuem **Shift**+**Alt**+**F7** a `Window.PreviousDocumentWindowNav` e **Alt**+**F7** a `Window.NextDocumentWindowNav`.

> [!NOTE]
> Se a combinação de configurações que você está usando ainda não tiver uma combinação de teclas de atalho atribuída a esse comando, você poderá atribuir seu próprio comando personalizado usando a página **Teclado** da caixa de diálogo **Opções**. Para obter mais informações, consulte [Identificar e personalizar atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).

### <a name="to-switch-to-a-specific-tool-window-in-the-ide"></a>Para mudar para uma janela de ferramentas específica no IDE

-   Pressione **ALT**+**F7** para exibir o **Navegador de IDE**. Mantenha pressionada a tecla **ALT** e pressione **F7** repetidamente até selecionar a janela para a qual você pretende mudar.

    > [!TIP]
    > Para inverter a ordem em que você percorre a lista **Janelas de Ferramentas Ativas**, mantenha pressionada as teclas **Shift**+**Alt** e pressione **F7**.

## <a name="see-also"></a>Consulte também

- [Personalizar layouts de janela](../ide/customizing-window-layouts-in-visual-studio.md)
- [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md)