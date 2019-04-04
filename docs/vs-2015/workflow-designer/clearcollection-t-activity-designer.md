---
title: ClearCollection&lt;T&gt; Designer de atividade | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 240e634115e7602c66d69f0dba9cfa52504dc89a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58923441"
---
# <a name="clearcollectionlttgt-activity-designer"></a>ClearCollection&lt;T&gt; Designer de atividade
O **ClearCollection\<T >** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.ClearCollection%601> atividade.  
  
## <a name="the-clearcollectiont-activity"></a>O ClearCollection\<T > atividade  
 A atividade de <xref:System.Activities.Statements.ClearCollection%601> limpa especificada uma coleção de todos os itens.  
  
### <a name="using-the-clearcollectiont-activity-designer"></a>Usando o ClearCollection\<T > Designer de atividade  
 O **ClearCollection\<T >** designer de atividade pode ser encontrado no **coleção** categoria do **caixa de ferramentas**, que é acessado clicando-se a  **Caixa de ferramentas** guia do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **ClearCollection\<T >** designer de atividade pode ser arrastado dos **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.ClearCollection%601> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de ClearCollection\<Int32 >. (Por padrão, o *TypeArgument* é **Int32**. Isso pode ser alterado na grade de propriedade.) O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **ClearCollection\<T >** designer de atividade ou nos **DisplayName** caixa da grade de propriedade. Outras propriedades devem ser editadas na grade de propriedade.  
  
### <a name="the-clearcollectiont-properties"></a>O ClearCollection\<T > Propriedades  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.ClearCollection%601> e descreve como elas são usadas no designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável opcional de atividade de <xref:System.Activities.Statements.ClearCollection%601> . O padrão é ClearCollection\<Int32 >. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|verdadeiro|Especifica a coleção a ser limpa os itens. Essa coleção é do tipo **ICollection\<TypeArgument >.** Para especificar a coleção, digite uma expressão do Visual Basic na grade de propriedade.|  
|*TypeArgument*|verdadeiro|Especifica o tipo T de itens contidos em <xref:System.Collections.Generic.ICollection%601>. Por padrão, isso *TypeArgument* tipo está definido como **Int32**. Para alterar o tipo, altere o valor da *TypeArgument* na caixa de combinação na grade de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [coleção](../workflow-designer/collection-activity-designers.md)   
 [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)   
 [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)   
 [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)