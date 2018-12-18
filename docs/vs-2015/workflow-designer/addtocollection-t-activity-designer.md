---
title: AddToCollection&lt;T&gt; Designer de atividade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.AddToCollection`1.UI
ms.assetid: f7fc0702-164e-4370-8946-bb2f9f9384b7
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 009f9f90c5cd22e5cf0da4240d008ce3dc1bb4ca
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49304416"
---
# <a name="addtocollectionlttgt-activity-designer"></a>AddToCollection&lt;T&gt; Designer de atividade
O **AddToCollection\<T >** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.AddToCollection%601> atividade.  
  
## <a name="the-addtocollectiont-activity"></a>O AddToCollection\<T > atividade  
 A atividade de <xref:System.Activities.Statements.AddToCollection%601> adiciona um item a uma coleção.  
  
### <a name="using-the-addtocollectiont-activity-designer"></a>Usando o AddToCollection\<T > Designer de atividade  
 O **AddToCollection\<T >** designer de atividade pode ser encontrado no **coleção** categoria do **caixa de ferramentas**, que é acessado clicando-se a  **Caixa de ferramentas** guia do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **AddToCollection\<T >** designer de atividade pode ser arrastado dos **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.AddToCollection%601> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de AddToCollection\<Int32 >. (Por padrão, o *TypeArgument* é **Int32**. Isso pode ser alterado na grade de propriedade.) O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **AddToCollection\<T >** designer de atividade ou nos **DisplayName** caixa da grade de propriedade. Outras propriedades devem ser editadas na grade de propriedade.  
  
### <a name="the-addtocollectiont-properties"></a>O AddToCollection\<T > Propriedades  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.AddToCollection%601> e descreve como elas são usadas no designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.AddToCollection%601> . O padrão é AddToCollection\<Int32 >. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.AddToCollection%601.Item%2A>|verdadeiro|O item a ser adicionado à coleção\<T >. Este item é do tipo *T*, que é do tipo *TypeArgument*. Para especificar o item, digite uma expressão do Visual Basic na grade de propriedade.|  
|<xref:System.Activities.Statements.AddToCollection%601.Collection%2A>|verdadeiro|A coleção para que o item deve ser adicionado. Essa coleção é do tipo **ICollection\<TypeArgument >**. Para especificar a coleção, digite uma expressão do Visual Basic na grade de propriedade.|  
|*TypeArgument*|verdadeiro|O tipo T de itens contidos em <xref:System.Collections.Generic.ICollection%601>. Por padrão, isso *TypeArgument* tipo está definido como **Int32**. Para alterar o tipo, altere o valor da *TypeArgument* na caixa de combinação na grade de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [coleção](../workflow-designer/collection-activity-designers.md)   
 [AddToCollection\<T > Designer de atividade](../workflow-designer/addtocollection-t-activity-designer.md)   
 [ClearCollection\<T >](../workflow-designer/clearcollection-t-activity-designer.md)   
 [ExistsInCollection\<T >](../workflow-designer/existsincollection-t-activity-designer.md)   
 [RemoveFromCollection\<T >](../workflow-designer/removefromcollection-t-activity-designer.md)