---
title: Como definir opções de acessibilidade do IDE
description: Saiba como definir opções de acessibilidade no Visual Studio que deixarão o IDE (ambiente de desenvolvimento integrado) mais fácil de usar para todos, incluindo pessoas com deficiência visual para ler e pessoas com limitações na capacidade de escrever.
ms.date: 08/23/2019
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: how-to
helpviewer_keywords:
- accessibility [Visual Studio]
ms.assetid: ddc96c4c-0600-46c1-8267-7dce4c44ad24
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac857d961b1ae736645ba2cfda3f1ef5755d0fa1
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770282"
---
# <a name="how-to-set-ide-accessibility-options"></a>Como definir opções de acessibilidade do IDE

O Visual Studio inclui recursos que facilitam a leitura para pessoas com deficiência visual e a escrita para pessoas com destreza limitada. Por exemplo, você pode alterar o tamanho e a cor do texto em editores, modificar o tamanho do texto e dos botões nas barras de ferramentas e as configurações para ajudá-lo a concluir uma função ou instrução.

Além disso, o Visual Studio fornece suporte a layouts de teclado Dvorak, que torna os caracteres digitados com maior frequência mais acessíveis. Você também pode personalizar os atalhos de teclado padrão disponíveis com o Visual Studio. Para obter mais informações, consulte [Identificar e personalizar atalhos de teclado](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md).

> [!NOTE]
> As caixas de diálogo e os comandos de menu vistos podem ser diferentes daqueles descritos aqui, o que pode variar dependendo da edição ou das configurações ativas. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** . Para obter mais informações, confira [Redefinir as configurações](../environment-settings.md#reset-settings).

::: moniker range="vs-2017"

> [!TIP]
> Para saber mais sobre atualizações de acessibilidade recentes, confira a postagem no blog [Accessibility improvements in Visual Studio 2017 version 15.3](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/) (Aprimoramentos de acessibilidade no Visual Studio 2017 versão 15.3).

::: moniker-end

## <a name="editors-dialogs-and-tool-windows"></a>Editores, caixas de diálogo e janelas de ferramentas

Por padrão, caixas de diálogo e janelas de ferramentas no Visual Studio usam o mesmo tamanho de fonte e as mesmas cores do sistema operacional. As configurações de cor do quadro do IDE, das caixas de diálogo, das barras de ferramentas e das janelas de ferramentas são baseadas em um esquema de cores: clara ou escuro. Você pode alterar o tema de cor atual na [caixa de diálogo opções: ambiente > geral](../../ide/reference/general-environment-options-dialog-box.md).

Também é possível exibir janelas pop-up no modo de exibição de Código do editor. Essas janelas podem fornecer membros disponíveis no objeto atual e os parâmetros para concluir uma função ou instrução. Essas janelas podem ser úteis se você tiver dificuldades para digitar. No entanto, elas interferem no foco do editor de código, o que pode ser um problema para alguns usuários.

Veja como desativar as janelas pop-up:

1. No menu **Ferramentas**, escolha **Opções**.

1. Escolha **Editor de texto**  >  **todos os idiomas**  >  **geral**.

1. Desmarque as caixas de seleção **Listar membros automaticamente** e **Informações de parâmetros**.

É possível reorganizar as janelas no IDE (ambiente de desenvolvimento integrado) para se adequar melhor à maneira como você trabalha. Você pode encaixar, derivar, ocultar ou ocultar automaticamente cada janela de ferramentas. Saiba mais sobre como alterar os layouts das janelas em [Personalizar layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md).

### <a name="change-the-size-of-text"></a>Alterar o tamanho do texto

É possível alterar as configurações de janelas de ferramentas baseadas em texto, como as janelas **Comando**, **Imediato** e de **Saída**, usando **Ferramentas** > **Opções** > **Ambiente** > **Fontes e cores**.

Ao selecionar **[Todas as janelas de ferramentas de texto]** na lista suspensa **Mostrar configurações de**, a configuração padrão é listada como **Padrão** nas listas suspensas **Primeiro plano do item** e **Tela de fundo do item**. Escolha o botão **Personalizar** para alterar essas configurações.

Também é possível alterar as configurações de como o texto é exibido no editor. Veja como.

1. No menu **Ferramentas**, escolha **Opções**.

1. Escolha **Environment**  >  **fontes e cores**do ambiente.

1. Selecione uma opção no menu suspenso **Mostrar configurações de**.

    Para alterar o tamanho da fonte do texto em um editor, escolha **Editor de Texto**.

    Para alterar o tamanho da fonte do texto em janelas de ferramentas baseadas em texto, escolha **[Todas as janelas de ferramentas de texto]**.

    Para alterar o tamanho da fonte do texto das Dicas de Ferramentas de um editor, escolha **Dica de Ferramenta do Editor**.

    Para alterar o tamanho da fonte do texto em pop-ups de preenchimento de declaração, escolha **Preenchimento de declaração**.

1. Em **Exibir Itens**, selecione **Texto sem formatação**.

1. Em **Fonte**, selecione um novo tipo de fonte.

1. Em **Tamanho**, selecione um novo tamanho da fonte.

    > [!TIP]
    > Para redefinir o tamanho do texto em editores e janelas de ferramentas baseadas em texto, escolha **Usar Padrões**.

7. Selecione **OK**.

### <a name="change-the-colors-that-are-used-in-the-ide"></a>Alterando as cores usadas no IDE

Você pode optar por alterar as cores padrão de texto, indicadores de margem, espaços em branco e elementos de código no editor. Veja como.

1. No menu **Ferramentas**, escolha **Opções**.

1. Na pasta **Ambiente**, escolha **Fontes e Cores**.

1. Em **Mostrar configurações de**, escolha **Editor de Texto**.

1. Em **Exibir Itens**, selecione um item cuja exibição você precisa alterar, como **Texto sem formatação**, **Margem de Indicadores**, **Espaço em branco visível**, **Nome do Atributo HTML** ou **Atributo XML**.

1. Selecione configurações de exibição entre as opções a seguir: **Primeiro plano do item**, **Tela de fundo do item** e **Negrito**.

1. Selecione **OK**.

> [!TIP]
> Para usar cores de alto contraste para todas as janelas de aplicativos em seu sistema operacional, pressione **ALT esquerda**com + **SHIFT esquerda** + **PrtScn**. Feche e reabra o Visual Studio, se estiver aberto, para implementar completamente as cores de alto contraste.

## <a name="toolbars"></a>Barras de Ferramentas

Para melhorar a acessibilidade e a usabilidade da barra de ferramentas, você pode adicionar texto a botões da barra de ferramentas.

### <a name="to-assign-text-to-toolbar-buttons"></a>Para atribuir texto a botões da barra de ferramentas

1. No menu **Ferramentas**, escolha **Personalizar**.

1. Na caixa de diálogo **Personalizar**, selecione a guia **Comandos**.

1. Selecione **barra de ferramentas**e, em seguida, escolha o nome da barra de ferramentas que contém o botão para o qual você pretende exibir o texto.

1. Na lista, selecione o comando que deseja alterar.

1. Escolha **Modificar seleção**.

1. Escolha **Imagem e Texto**.

### <a name="to-modify-the-displayed-text-in-a-button"></a>Para modificar o texto exibido em um botão

1. Selecione **Modificar seleção** novamente.

1. Ao lado de **Nome**, forneça uma nova legenda para o botão selecionado.

## <a name="see-also"></a>Confira também

* [Recursos de acessibilidade do Visual Studio](../../ide/reference/accessibility-features-of-visual-studio.md)
* [Acessibilidade para Visual Studio para Mac](/visualstudio/mac/accessibility/)
* [Recursos para a criação de aplicativos acessíveis](../../ide/reference/resources-for-designing-accessible-applications.md)
