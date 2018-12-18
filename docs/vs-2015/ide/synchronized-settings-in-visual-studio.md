---
title: Configurações sincronizadas
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Environment.RoamingSettings
ms.assetid: a3d2ea29-be5d-4012-9820-44b06adbb7dd
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1b0ab4b0d006183f6be3c42626c022d45a2de4ce
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53067123"
---
# <a name="synchronized-settings-in-visual-studio"></a>Configurações sincronizadas no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você usa a mesma conta de personalização para entrar no Visual Studio em vários computadores, por padrão, as configurações são sincronizadas em todos os computadores.

## <a name="synchronized-settings"></a>Configurações sincronizadas
 Por padrão, as seguintes configurações são definidas.

-   As configurações de desenvolvimento (você precisa selecionar um conjunto de configurações durante a primeira execução do Visual Studio, mas você pode alterar a seleção a qualquer momento. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).)

-   As seguintes opções nas páginas **Ferramentas &#124; Opções**:

    -   **Tema** e configurações de uso de maiúsculas da barra de menus, na página de opções **Ambiente**, **Geral**

    -   Todas as configurações da página de opções **Ambiente**, **Fontes e Cores**

    -   Todos os atalhos de teclado, na página de opções **Ambiente**, **Teclado**

    -   Todas as configurações da página de opções **Ambiente, Guias e Janelas**

    -   Todas as configurações da página de opções **Ambiente**, **Inicialização**

    -   Todas as configurações das páginas de opções **Editor de Texto**

-   Todas as configurações das páginas de opções Designer XAML

-   Alias de comando definidos pelo usuário. Para obter mais informações sobre como definir aliases de comando, consulte [Aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

-   Layouts de janela definidos pelo usuário na página **Janela &#124; Gerenciar Layouts de Janela**

## <a name="turning-synchronized-settings-off-for-a-particular-computer"></a>Ativar sincronizado as configurações de um computador específico
 As configurações sincronizadas para o Visual Studio são ativadas por padrão. É possível desligar as configurações sincronizadas em um computador acessando a página **Ferramentas &#124; Opções &#124; Ambiente &#124; Configurações Sincronizadas** e desmarcando a caixa de seleção.  Por exemplo, se você decidir não sincronizar as configurações do Visual Studio no Computador A, todas as alterações de configuração feitas no Computador A não serão exibidas no Computador B ou C. Os Computadores B e C continuarão sendo sincronizados entre si, mas não com o Computador A.

## <a name="synchronizing-settings-across-visual-studio-family-products-and-editions"></a>Sincronização de configurações entre as edições e produtos da família Visual Studio
 As configurações podem ser sincronizadas em qualquer edição do Visual Studio 2015, incluindo as edições Express e da comunidade. As configurações também são sincronizadas em produtos da família Visual Studio, como o Blend. No entanto, cada um desses produtos da família pode ter suas próprias configurações que não são compartilhadas com o Visual Studio. Por exemplo, as configurações específicas ao Blend no computador A serão compartilhadas com o Blend no computador B, mas não com o Visual Studio no computador A ou B.

> [!WARNING]
>  As configurações não são sincronizadas entre o Visual Studio 2013 e Visual Studio 2015. Na primeira vez que você abrir o Visual Studio 2015, as configurações do Visual Studio 2013 são migradas, mas eles não podem ser migrados de volta para Visual Studio 2013 depois disso.

## <a name="see-also"></a>Consulte também
 [Personalizando o IDE](../ide/personalizing-the-visual-studio-ide.md)
