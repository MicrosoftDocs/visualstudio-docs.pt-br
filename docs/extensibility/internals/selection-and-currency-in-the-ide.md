---
title: Seleção e moeda no IDE | Microsoft Docs
description: Saiba como o VSPackages faz parte do controle de moeda. O IDE do Visual Studio mantém informações sobre os objetos selecionados no momento usando o contexto de seleção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0fb65a63b99f625f8d32af8436db753a0f17322e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080899"
---
# <a name="selection-and-currency-in-the-ide"></a>Seleção e moeda no IDE
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) mantém informações sobre os objetos selecionados no momento usando o *contexto* de seleção. Com o contexto de seleção, VSPackages pode participar do controle de moeda de duas maneiras:

- Propagando informações de moeda sobre o VSPackages para o IDE.

- Monitorando as seleções atualmente ativas do usuário no IDE.

## <a name="selection-context"></a>Contexto de seleção
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE mantém o controle global da moeda IDE em seu próprio objeto de contexto de seleção global. A tabela a seguir mostra os elementos que compõem o contexto de seleção.

|Elemento|Descrição|
|-------------|-----------------|
|Hierarquia atual|Normalmente, o projeto atual; uma hierarquia atual nula indica que a solução como um todo é atual.|
|ItemID atual|O item selecionado na hierarquia atual; Quando há várias seleções em uma janela de projeto, pode haver vários itens atuais.|
|Atualizados `SelectionContainer`|Mantém um ou mais objetos para os quais o janela Propriedades deve exibir as propriedades.|

 Além disso, o ambiente mantém duas listas globais:

- Uma lista de identificadores de comando de interface do usuário ativas

- Uma lista de tipos de elementos atualmente ativos.

### <a name="window-types-and-selection"></a>Tipos de janela e seleção
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE organiza as janelas em dois tipos gerais:

- Janelas de tipo de hierarquia

- Janelas de quadros, como janelas de ferramentas e documentos

  O IDE rastreia a moeda de forma diferente para cada um desses tipos de janela.

  A janela de tipo de projeto mais comum é o Gerenciador de soluções, que o IDE controla. Uma janela de tipo de projeto rastreia a hierarquia global e ItemID do contexto de seleção global, e a janela depende da seleção do usuário para determinar a hierarquia atual. Para janelas de tipo de projeto, o ambiente fornece o serviço global <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> , por meio do qual VSPackages pode monitorar os valores atuais para elementos abertos. A navegação de propriedade no ambiente é orientada por esse serviço global.

  Janelas de quadros, por outro lado, usam o DocObject dentro da janela do quadro para enviar por push o valor de SelectionContext (a Hierarchy/ItemID/SelectionContainer trio). . Janelas de quadros usam o serviço <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> para essa finalidade. O DocObject pode enviar somente valores para o contêiner de seleção, deixando os valores locais para Hierarchy e ItemID inalterados, como é típico para documentos filho MDI.

### <a name="events-and-currency"></a>Eventos e moeda
 Podem ocorrer dois tipos de eventos que afetam a noção de moeda do ambiente:

- Eventos que são propagados para o nível global e alteram o contexto de seleção do quadro da janela. Exemplos desse tipo de evento incluem uma janela filho MDI sendo aberta, uma janela de ferramenta global sendo aberta ou uma janela de ferramenta do tipo projeto que está sendo aberta.

- Eventos que alteram os elementos rastreados dentro do contexto de seleção do quadro da janela. Os exemplos incluem alterar a seleção em um DocObject ou alterar a seleção em uma janela de tipo de projeto.

## <a name="see-also"></a>Confira também
- [Objetos de contexto da seleção](../../extensibility/internals/selection-context-objects.md)
- [Comentários para o usuário](../../extensibility/internals/feedback-to-the-user.md)
