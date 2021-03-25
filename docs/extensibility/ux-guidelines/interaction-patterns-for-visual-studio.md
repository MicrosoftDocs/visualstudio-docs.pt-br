---
title: Padrões de interação do Visual Studio | Microsoft Docs
description: Saiba mais sobre a biblioteca de padrões comuns de interação que você pode usar ao criar novos recursos para o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 05/13/2020
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 215fa0145a342820320980f629bb35678ce09680
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072930"
---
# <a name="interaction-patterns-for-visual-studio"></a>Padrões de interação para Visual Studio
## <a name="overview"></a>Visão geral
 Um padrão de design, em geral, é o núcleo de um design que pode ser aplicado em situações específicas para resolver problemas com conjuntos de restrições semelhantes. Os designers de recursos e sistemas usam esses padrões de design como pontos de partida, que podem ser adaptados para sua situação específica.

 O Visual Studio tem uma biblioteca de padrões comuns de interação que devem ser considerados ao criar novos recursos. Há dois contextos principais para nossos padrões de design: cliente do Visual Studio (devenv) e GitHub Codespaces (anteriormente conhecido como Visual Studio online). Para alguns problemas de design, há um padrão onipresente que funciona bem em todas as situações. Em muitos casos, no entanto, a solução pode ser diferente para a interface do usuário que está sendo apresentada em um navegador e que está hospedada em um aplicativo cliente.

### <a name="visual-studio-client-pattern-types"></a>Tipos de padrões de cliente do Visual Studio

|Tipo de padrão|Descrição|Exemplos|
|------------------|-----------------|--------------|
|**Padrões de nível de aplicativo**|Padrões de alto nível comuns ao aplicativo, determinando ou exibindo o contexto do aplicativo e contendo padrões de composição e controle dentro deles|-Janelas de ferramentas<br />-Janelas de documentos|
|**Padrões de composição**|Padrões comuns que podem abranger padrões de aplicativo ou um padrão reconhecido composto por vários controles em uma configuração distinta|-Exibição de alternância<br />-Listar construtores<br />-Exibindo dados<br />-Notificações<br />-Validação<br />-Modelos de seleção|
|**Padrões de controle**|Informações específicas sobre como se espera que os controles de nível baixo se comportem|-Exibições de árvore<br />-Edição em um controle de grade|

## <a name="application-patterns"></a>Padrões de aplicativo
 Em um alto nível, a interface do Visual Studio é composta por várias janelas, caixas de diálogo, comandos e barras de ferramentas em um único IDE. A hierarquia do Visual Studio determina os menus de contexto e de unidades. Os principais pontos de integração na interface do usuário do IDE são janelas de documentos, janelas de ferramentas, projetos, a estrutura de comandos, o editor de texto, a caixa de ferramentas, a janela Propriedades e as opções de > de ferramentas.

 Há padrões de uso básicos para cada um dos principais pontos de integração na interface do usuário do IDE:

- [Menus e comandos para Visual Studio](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Padrões de aplicativo para Visual Studio](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [Interações com a janela](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [Janelas de ferramentas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [Convenções do editor de documento](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [Diálogos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [Projetos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>Padrões de controle comuns
 Padrões de controle são principalmente sobre como os controles individuais devem se comportar. Essa é uma área na qual a consistência é mais crítica.

 Os controles mais comuns no Visual Studio devem seguir as diretrizes do Windows para desktop. Nossas diretrizes incluem apenas áreas nas quais precisamos aumentar as convenções comuns com interações específicas do Visual Studio ou locais em que substituímos as diretrizes inteiramente para personalizar o Visual Studio para atender às necessidades de nossos usuários sofisticados.

- [Padrões de controle comuns para Visual Studio](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [Controles comuns](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [Botões e hiperlinks](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>Padrões de composição
 Há várias maneiras que os usuários esperam realizar tarefas. Sempre que possível, os recursos devem ser projetados para usar esses padrões tanto para a interação quanto para o Design Visual.

 Embora existam muitos padrões compostos no Visual Studio, algumas das mais importantes em relação à consistência são:

- [Padrões de composição para Visual Studio](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [Interface do usuário e inspeção do objeto](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [Modelos de seleção](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [Configurações de persistência e salvamento](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [Entrada por toque](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
