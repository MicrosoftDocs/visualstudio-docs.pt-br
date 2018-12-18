---
title: ExistsInCollection&lt;T&gt; Designer de atividade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: fa4de7e599e2707e1b949536c1d94e32e3eb33e1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49177717"
---
# <a name="existsincollectionlttgt-activity-designer"></a>ExistsInCollection&lt;T&gt; Designer de atividade
O **ExistsInCollection\<T >** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.ExistsInCollection%601> atividade.  
  
## <a name="the-existsincollectiont-activity"></a>O ExistsInCollection\<T > atividade  
 A atividade de <xref:System.Activities.Statements.ExistsInCollection%601> determina se um item específico existe em uma coleção específico.  
  
### <a name="using-the-existsincollectiont-activity-designer"></a>Usando o ExistsInCollection\<T > Designer de atividade  
 O **ExistsInCollection\<T >** designer de atividade pode ser encontrado no **coleção** categoria do **caixa de ferramentas**, que é acessado clicando-se a  **Caixa de ferramentas** guia de [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **ExistsInCollection\<T >** designer de atividade pode ser arrastado dos **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como dentro de um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.ExistsInCollection%601> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de ExistsInCollection\<Int32 >. (Por padrão, o *TypeArgument* é **Int32**. Pode ser alterado na grade de propriedade.)  O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **ExistsInCollection\<T >** designer de atividade ou nos **DisplayName** caixa da grade de propriedade. Outras propriedades devem ser editadas na grade de propriedade.  
  
### <a name="the-existsincollectiont-properties"></a>O ExistsInCollection\<T > Propriedades  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.ExistsInCollection%601> e descreve como elas são usadas no designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.ExistsInCollection%601> . O padrão é ExistsInCollection\<Int32 >. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|verdadeiro|O item a ser adicionado à coleção\<T >. Este item é do tipo *T* é do tipo *TypeArgument*. Para especificar o item, digite uma expressão do Visual Basic na grade de propriedade.|  
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|verdadeiro|A coleção para que o item deve ser adicionado. Essa coleção é do tipo **ICollection\<TypeArgument >.** Para especificar a coleção, digite uma expressão do Visual Basic na grade de propriedade.|  
|*TypeArgument*|verdadeiro|O tipo T de itens contidos em <xref:System.Collections.Generic.ICollection%601>. Por padrão, isso *TypeArgument* tipo está definido como **Int32**. Para alterar o tipo, altere o valor da *TypeArgument* na caixa de combinação na grade de propriedade.|  
|<xref:System.Activities.Activity%601.Result%2A>|False|Um valor que indica se o item especificado existe na coleção. Para especificar uma variável para associar ao resultado, digite uma variável do Visual Basic na grade de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [coleção](../workflow-designer/collection-activity-designers.md)   
 [AddToCollection\<T >](../workflow-designer/addtocollection-t-activity-designer.md)   
 [ClearCollection\<T >](../workflow-designer/clearcollection-t-activity-designer.md)   
 [RemoveFromCollection\<T >](../workflow-designer/removefromcollection-t-activity-designer.md)