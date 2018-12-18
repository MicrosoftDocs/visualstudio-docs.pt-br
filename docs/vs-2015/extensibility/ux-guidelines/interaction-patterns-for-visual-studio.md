---
title: Padrões de interação para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
caps.latest.revision: 5
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c6dcb0ccb6a8793649c0b12b6851ba58b9374da9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779366"
---
# <a name="interaction-patterns-for-visual-studio"></a>Padrões de interação para Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="overview"></a>Visão geral  
 Um padrão de design, em geral, é o núcleo de um design que pode ser aplicado em situações específicas para resolver problemas com conjuntos semelhantes de restrições. Designers de recurso e o sistema usam esses padrões de design como partida pontos, que, em seguida, podem ser adaptados à sua situação específica.  
  
 O Visual Studio tem uma biblioteca de padrões comuns de interação que devem ser considerados ao criar novos recursos. Há dois contextos de núcleo para nossos padrões de design: cliente do Visual Studio (devenv) e o Visual Studio Online. Para alguns problemas de design, há um padrão de todos os lugares que funciona bem em todas as situações. Em muitos casos, no entanto, a solução pode ser diferente para a interface do usuário que está sendo apresentado em um navegador e que está hospedado em um aplicativo cliente.  
  
### <a name="visual-studio-client-pattern-types"></a>Tipos de padrão de cliente do Studio Visual  
  
|Tipo de padrão|Descrição|Exemplos|  
|------------------|-----------------|--------------|  
|**Padrões de nível de aplicativo**|Padrões de alto nível comuns para o aplicativo, determinando ou exibindo o contexto do aplicativo e que contém a composição e padrões de controle dentro deles|-Janelas de ferramentas<br />– Janelas de documento|  
|**Padrões de composição**|Padrões comuns que podem abranger em padrões de aplicativo ou um padrão reconhecido composto de vários controles em uma configuração distinta|-Exibir a exibição<br />-Construtores de lista<br />-Exibindo dados<br />-Notificações<br />-Validação<br />-Modelos seleção|  
|**Padrões de controle**|Informações específicas sobre controles de baixo nível como devem se comportar|-Modos de exibição de árvore<br />-Edição dentro de um controle de grade|  
  
## <a name="application-patterns"></a>Padrões de aplicativo  
 Em um alto nível, a interface do Visual Studio consiste em vários windows, as caixas de diálogo, comandos e barras de ferramentas dentro de um único IDE. A hierarquia do Visual Studio determina os menus de contexto e unidades. Os pontos de integração principais na interface do usuário do IDE são janelas de documentos, janelas de ferramentas, projetos, a estrutura de comando, o editor de texto, a caixa de ferramentas, a janela Propriedades e ferramentas > Opções.  
  
 Há padrões de uso básico para cada um dos pontos de integração principais na interface do usuário do IDE:  
  
-   [Menus e comandos para Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)  
  
-   [Padrões de aplicativo para Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)  
  
    -   [Interações de janela](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)  
  
    -   [Janelas de ferramentas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)  
  
    -   [Convenções do editor de documento](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)  
  
    -   [Caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)  
  
    -   [Projetos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)  
  
## <a name="common-control-patterns"></a>Padrões de controle comum  
 Padrões de controle são principalmente sobre os controles individuais como esperado se comportar. Esta é uma área em que a consistência é mais crítica.  
  
 Controles mais comuns no Visual Studio devem seguir as diretrizes do Windows de área de trabalho. Nossas diretrizes incluem apenas as áreas em que precisamos ampliar a convenções comuns com interações específicas do Visual Studio, ou locais em que podemos substituem as diretrizes inteiramente para adequar o Visual Studio para atender às necessidades de nossos usuários sofisticados.  
  
-   [Padrões de controle comuns para Visual Studio](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)  
  
    -   [Controles comuns](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)  
  
    -   [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)  
  
    -   [Hiperlinks e botões](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)  
  
## <a name="composite-patterns"></a>Padrões de composição  
 Há várias maneiras que os usuários esperam para realizar tarefas. Sempre que possível, os recursos devem ser projetados para usar esses padrões para interação do e design visual.  
  
 Embora haja muitos padrões de composição dentro do Visual Studio, alguns dos mais importantes com relação à consistência são:  
  
-   [Padrões de composição para Visual Studio](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)  
  
    -   [Interface do usuário no objeto e inspecionar](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)  
  
    -   [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)  
  
    -   [Salvando as configurações e persistência](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)  
  
    -   [Entrada de toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)

