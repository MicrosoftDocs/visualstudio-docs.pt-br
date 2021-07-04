---
title: Saiba mais sobre a janela de ferramentas de Gerenciador de Soluções
description: saiba como você pode usar a janela de ferramentas do Gerenciador de Soluções no Visual Studio para criar & gerenciar seus arquivos, projetos e soluções.
ms.date: 06/29/2021
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
helpviewer_keywords:
- solution explorer [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fbbae8b974a7e88abffd9a12eb253dfea6c7165b
ms.sourcegitcommit: 8fb1500acb7e6314fbb6b78eada78ef5d61d39bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2021
ms.locfileid: "113280497"
---
# <a name="how-to-use-solution-explorer"></a>Como usar Gerenciador de Soluções

Você pode usar a janela de ferramentas de Gerenciador de Soluções para criar & gerenciar suas soluções e projetos e exibir & interagir com seu código. Neste artigo, detalharemos as opções de interface do usuário que o ajudarão a fazer isso.

> [!NOTE]
> Este tópico aplica-se apenas ao Visual Studio no Windows.

## <a name="solution-explorer-tool-window"></a>Janela de ferramentas do Gerenciador de Soluções

para começar, vamos dar uma olhada na janela de ferramentas de Gerenciador de Soluções no [IDE Visual Studio](../get-started/visual-studio-ide.md), com uma solução aberta de console C# que tem dois projetos.

[![A janela de ferramentas de Gerenciador de Soluções no Visual Studio.](media/solution-explorer-tool-window.png)](media/solution-explorer-tool-window.png#lightbox)

A janela de ferramentas contém os seguintes elementos da interface do usuário (interface de usuários):

- **Barra de menus**, onde você pode controlar a aparência dos arquivos
- **Barra de pesquisa**, onde você pode pesquisar arquivos e tipos de arquivos específicos
- **Janela principal**, onde você pode exibir e gerenciar seus arquivos, projetos & soluções
- **Nó da solução**, onde você pode gerenciar suas soluções
- **Project nó**, onde você pode gerenciar seus projetos
- **Nó Dependencies**, onde você pode gerenciar sua solução & dependências do projeto
- **Nó de programa**, no qual você pode exibir, editar e gerenciar seu programa ou aplicativo (aplicativo)
- **[guia de alterações do git](../version-control/git-with-visual-studio.md?view=vs-2019&preserve-view=true#git-changes-window)**, em que você pode usar o git & GitHub em Visual Studio para colaborar em projetos com sua equipe

> [!TIP]
> se você não vir a janela de ferramentas Gerenciador de Soluções, poderá abri-la na barra de menus Visual Studio usando **View**  >  **Gerenciador de Soluções** ou pressionando **Ctrl** + **Alt** + **L**.

## <a name="solution-explorer-menu-bar"></a>Barra de menus Gerenciador de Soluções

Para continuar, vamos examinar mais de perto a barra de menus Gerenciador de Soluções.

![A barra de menus Gerenciador de Soluções no Visual Studio.](media/solution-explorer-menu-bar.png)

A barra de menus contém os seguintes elementos da interface do usuário, da esquerda para a direita:

- Botão **voltar** , para alternar entre os resultados da pesquisa
- Botão **encaminhar** , para alternar entre os resultados da pesquisa
- Botão **página inicial** , para retornar ao modo de exibição padrão
- Botão **alternar** para alternar entre as soluções e as exibições disponíveis
- Botão de **filtro de alterações pendentes** & menu suspenso para exibir arquivos ou arquivos abertos com alterações pendentes
- Botão **sincronizar com o documento ativo** , para localizar um arquivo do editor de código
- Botão **Atualizar** , que aparece somente quando você seleciona uma dependência, como uma função ou um pacote
- Botão **recolher tudo** para recolher a exibição de arquivo na janela principal
- Botão **Mostrar todos os arquivos** , para exibir todos os arquivos, incluindo [projetos descarregados](filtered-solutions.md#toggle-unloaded-project-visibility)
- Botão **Propriedades** , para exibir e alterar as configurações de arquivos e componentes específicos
- Botão **Visualizar itens selecionados** para exibir um arquivo ou componente selecionado no editor de código

### <a name="solution-explorer-right-click-context-menu"></a>Gerenciador de Soluções menu de contexto de clique com o botão direito do mouse

No Gerenciador de Soluções, há várias propriedades de arquivo com as quais você pode interagir usando o menu de contexto de clique com o botão direito do mouse. Para obter mais informações sobre as opções de menu de contexto de clique com o botão direito do mouse, consulte a página [gerenciar o projeto e as propriedades da solução](managing-project-and-solution-properties.md) .

## <a name="see-also"></a>Confira também

- [O que são soluções e projetos no Visual Studio?](solutions-and-projects-in-visual-studio.md)
- [Personalizar layouts de janela no Visual Studio](customizing-window-layouts-in-visual-studio.md)
