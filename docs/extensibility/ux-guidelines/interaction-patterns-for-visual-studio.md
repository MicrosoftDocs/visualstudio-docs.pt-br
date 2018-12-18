---
title: Padrões de interação para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 094e16fea46e459dd64338ffa5daf3f7b98afb90
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31142426"
---
# <a name="interaction-patterns-for-visual-studio"></a>Padrões de interação para Visual Studio
## <a name="overview"></a>Visão geral  
 Um padrão de design, em geral, é o núcleo de um design que pode ser aplicado em situações específicas para solucionar problemas com conjuntos semelhantes de restrições. Designers de recurso e o sistema usam esses padrões de design como iniciando pontos, que podem ser adaptados para sua situação específica.  
  
 O Visual Studio tem uma biblioteca de padrões comuns de interação que devem ser considerados ao criar novos recursos. Há dois contextos de núcleo para nossos padrões de design: cliente Visual Studio (devenv) e Visual Studio Online. Para alguns problemas de design, há um padrão de todos os lugares que funciona bem em todas as situações. Em muitos casos, no entanto, a solução pode ser diferente para a interface do usuário que está sendo apresentado em um navegador e que está hospedado em um aplicativo cliente.  
  
### <a name="visual-studio-client-pattern-types"></a>Tipos de padrão do Visual Studio cliente  
  
|Tipo de padrão|Descrição|Exemplos|  
|------------------|-----------------|--------------|  
|**Padrões de nível de aplicativo**|Alto nível padrões comuns para o aplicativo, determinando ou exibindo o contexto do aplicativo e que contém a composição e padrões de controle dentro deles|-Janelas de ferramenta<br />-Janelas de documento|  
|**Padrões compostos**|Padrões comuns que podem abranger em padrões de aplicativo ou um padrão reconhecido composta por vários controles em uma configuração distinta|-Alternar exibição<br />-Construtores de lista<br />-Exibindo dados<br />-Notificações<br />-Validação<br />-Modelos de seleção|  
|**Padrões de controle**|Espera-se que as especificações sobre controles de baixo nível como se comportam|-Modos de exibição de árvore<br />-Edição em um controle de grade|  
  
## <a name="application-patterns"></a>Padrões de aplicativo  
 Em um nível alto, a interface do Visual Studio consiste em várias janelas, caixas de diálogo, comandos e barras de ferramentas dentro de um único IDE. A hierarquia do Visual Studio determina os menus de contexto e unidades. Os pontos de integração da chave na interface do usuário do IDE são janelas de documentos, janelas de ferramentas, projetos, a estrutura do comando, o editor de texto, a caixa de ferramentas, a janela Propriedades e ferramentas > Opções.  
  
 Há padrões de uso básico para cada um dos pontos de integração da chave na interface do usuário do IDE:  
  
-   [Menus e comandos para Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)  
  
-   [Padrões de aplicativo para Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)  
  
    -   [Interações de janela](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)  
  
    -   [Janelas de ferramentas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)  
  
    -   [Convenções de editor do documento](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)  
  
    -   [Caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)  
  
    -   [Projetos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)  
  
## <a name="common-control-patterns"></a>Padrões de controle comum  
 Padrões de controle são principalmente sobre os controles individuais como esperado se comporta. Esta é uma área em que a consistência é mais crítica.  
  
 Controles mais comuns no Visual Studio devem seguir as diretrizes do Windows de área de trabalho. Nossas diretrizes incluem apenas áreas em que precisamos ampliar a convenções comuns com as interações do Visual Studio específicos ou locais em que podemos substituem as diretrizes inteiramente para personalizar o Visual Studio para atender às necessidades de nossos usuários sofisticados.  
  
-   [Padrões de controle comuns para Visual Studio](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)  
  
    -   [Controles comuns](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)  
  
    -   [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)  
  
    -   [Hiperlinks e botões](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)  
  
## <a name="composite-patterns"></a>Padrões compostos  
 Há várias maneiras que os usuários esperam para realizar tarefas. Sempre que possível, os recursos devem ser criados para usar esses padrões para interação e design visual.  
  
 Embora haja muitos padrões compostos no Visual Studio, algumas das mais importantes com relação a consistência são:  
  
-   [Padrões de composição para Visual Studio](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)  
  
    -   [Interface do usuário no objeto e inspecionar](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)  
  
    -   [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)  
  
    -   [Persistência e salvar as configurações](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)  
  
    -   [Entrada de toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)