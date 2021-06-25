---
title: Padrões de interação para Visual Studio | Microsoft Docs
description: Saiba mais sobre a biblioteca de padrões comuns de interação que você pode usar ao criar novos recursos para Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 05/13/2020
ms.topic: reference
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13a2ec4332cf8010dc5d214dfd61936725ac2063
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900545"
---
# <a name="interaction-patterns-for-visual-studio"></a>Padrões de interação para Visual Studio
## <a name="overview"></a>Visão geral
 Um padrão de design, em geral, é o núcleo de um design que pode ser aplicado em situações específicas para resolver problemas com conjuntos semelhantes de restrições. Os designers de recursos e de sistema usam esses padrões de design como pontos de partida, que podem ser adaptados à sua situação específica.

 Visual Studio tem uma biblioteca de padrões comuns de interação que devem ser considerados ao criar novos recursos. Há dois contextos principais para nossos padrões de design: Visual Studio Client (devenv) e Codespaces do GitHub (anteriormente Visual Studio Online). Para alguns problemas de design, há um padrão onipresente que funciona bem em todas as situações. Em muitos casos, no entanto, a solução pode ser diferente para a interface do usuário que está sendo apresentada em um navegador e a que está hospedada em um aplicativo cliente.

### <a name="visual-studio-client-pattern-types"></a>Visual Studio padrão do cliente

|Tipo de padrão|Descrição|Exemplos|
|------------------|-----------------|--------------|
|**Padrões no nível do aplicativo**|Padrões de alto nível comuns ao aplicativo, determinando ou exibindo o contexto do aplicativo e contendo padrões de composição e controle dentro deles|– Janelas de ferramentas<br />– Janelas de documentos|
|**Padrões compostos**|Padrões comuns que podem abranger padrões de aplicativo ou um padrão reconhecido com vários controles em uma configuração distinta|– Exibir alternação<br />– Construtores de lista<br />– Exibindo dados<br />- Notificações<br />- Validação<br />– Modelos de seleção|
|**Padrões de controle**|Especificações sobre como os controles de baixo nível devem se comportar|– Exibições de árvore<br />- Edição em um controle de grade|

## <a name="application-patterns"></a>Padrões de aplicativo
 Em um alto nível, a Visual Studio interface do usuário inclui várias janelas, caixas de diálogo, comandos e barras de ferramentas em um único IDE. A Visual Studio de dados determina o contexto e os menus de unidades. Os principais pontos de integração na interface do usuário do IDE são janelas de documentos, janelas de ferramentas, projetos, estrutura de comando, editor de texto, caixa de ferramentas, janela Propriedades e Ferramentas > Opções.

 Há padrões de uso básicos para cada um dos principais pontos de integração na interface do usuário do IDE:

- [Menus e comandos para Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Padrões de aplicativo para Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [Interações de janela](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [Janelas de ferramentas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [Convenções do editor de documentos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [Diálogos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [Projetos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>Padrões de controle comuns
 Os padrões de controle são principalmente sobre como os controles individuais devem se comportar. Essa é uma área na qual a consistência é mais crítica.

 Os controles mais comuns no Visual Studio devem seguir as diretrizes do Windows da Área de Trabalho. Nossas diretrizes incluem apenas áreas nas quais precisamos aumentar as convenções comuns com interações específicas do Visual Studio ou locais em que as diretrizes são superadas inteiramente para adaptar Visual Studio para atender às necessidades de nossos usuários sofisticados.

- [Padrões de controle comuns para Visual Studio](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [Controles comuns](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [Botões e hiperlinks](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>Padrões compostos
 Há várias maneiras pelas quais os usuários esperam realizar tarefas. Sempre que possível, os recursos devem ser projetados para usar esses padrões para interação e design visual.

 Embora haja muitos padrões compostos dentro Visual Studio, alguns dos mais importantes em relação à consistência são:

- [Padrões de composição para Visual Studio](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [Interface do usuário no objeto e espiar](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [Persistência e configurações de salvação](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [Entrada de toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
