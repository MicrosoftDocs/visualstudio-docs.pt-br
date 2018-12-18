---
title: Designer de fluxo de trabalho - RemoveFromCollection&lt;T&gt; Designer de atividade
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.RemoveFromCollection`1.UI
ms.assetid: 6617ba26-c8bc-4aed-b746-112bf490d288
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 415d03ffda6bbd2e839354b4f7cb143337ab08c8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49891356"
---
# <a name="removefromcollectiont-activity-designer"></a>RemoveFromCollection\<T > Designer de atividade

O **RemoveFromCollection\<T >** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.RemoveFromCollection%601> atividade.

## <a name="the-removefromcollectiontactivity"></a>O RemoveFromCollection\<T > atividade

A atividade de <xref:System.Activities.Statements.RemoveFromCollection%601> remover um item específico de uma coleção específico.

### <a name="using-the-removefromcollectiont-activity-designer"></a>Usando o RemoveFromCollection\<T > Designer de atividade

Acesso a **RemoveFromCollection\<T >** designer de atividade no **coleção** categoria do **caixa de ferramentas**.
O **RemoveFromCollection\<T >** designer de atividade pode ser arrastado dos **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como dentro de um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.RemoveFromCollection%601> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de RemoveFromCollection < Int32\>. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **RemoveFromCollection < T\>**  designer de atividade ou nos **DisplayName** caixa da grade de propriedade. Outras propriedades devem ser editadas na grade de propriedade.

### <a name="the-removefromcollectiont-properties"></a>O RemoveFromCollection < T\> propriedades

A tabela a seguir mostra o <xref:System.Activities.Statements.RemoveFromCollection%601> propriedades e descreve como elas são usadas no designer:

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável opcional de atividade de <xref:System.Activities.Statements.RemoveFromCollection%601> . O padrão é o RemoveFromCollection < Int32\>.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Item%2A>|verdadeiro|O item a ser removido dos **coleta\<T >**. Este item é do tipo *T*, que é do tipo *TypeArgument*. Para especificar o item, digite uma expressão do Visual Basic na grade de propriedade.|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Collection%2A>|verdadeiro|A coleção da qual o item deve ser removido. Essa coleção é do tipo **ICollection < TypeArgument\>.** Para especificar a coleção, digite uma expressão do Visual Basic na grade de propriedade.|
|*TypeArgument*|verdadeiro|O tipo T de itens contidos em <xref:System.Collections.Generic.ICollection%601>. Por padrão, isso *TypeArgument* tipo está definido como **Int32**. Para alterar o tipo, altere o valor da *TypeArgument* na caixa de combinação na grade de propriedade.|
|<xref:System.Activities.Activity%601.Result%2A>|False|Um valor que indica se o item especificado foi removido da coleção. Para especificar uma variável para associar ao resultado, digite uma variável na grade de propriedade|

## <a name="see-also"></a>Consulte também

- [Coleção](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T >](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T >](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T >](../workflow-designer/existsincollection-t-activity-designer.md)