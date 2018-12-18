---
title: Designer de atividade Assign | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: c27d70f7dbff9d7f9d30d7dda34c5c2c98bfe891
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49281262"
---
# <a name="assign-activity-designer"></a>Atribua o designer de atividades
O **atribua** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Assign> atividade.  
  
## <a name="the-assign-activity"></a>A atividade atribuir  
 A atividade de <xref:System.Activities.Statements.Assign> atribui um valor a uma variável ou um argumento.  
  
### <a name="using-the-assign-activity-designer"></a>Usando o designer de atividade atribuir  
 O **atribuir** designer de atividade pode ser encontrado na **primitivos** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia (como alternativa, selecione **caixa de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **atribua** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície em que nunca atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.Assign> atividade com um padrão **DisplayName** de Assign. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **atribuir** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-assign-properties"></a>As propriedades atribuir  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Assign> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e algumas delass podem ser editadas na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Assign> . O padrão é atribui. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.Assign.To%2A>|verdadeiro|A variável ou o argumento para que <xref:System.Activities.Statements.Assign.Value%2A> é atribuído. Isso deve ser um identificador válido Visual Basic. Para definir a propriedade, digite uma expressão do Visual Basic na **para** caixa sobre o **atribuir** atividade designer ou na grade de propriedade.|  
|<xref:System.Activities.Statements.Assign.Value%2A>|verdadeiro|O valor que é atribuído à variável. Para definir a <xref:System.Activities.Statements.Assign.Value%2A>, digite uma expressão do Visual Basic na **valor** caixa no **atribuir** atividade designer ou na grade de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Primitivos](../workflow-designer/primitives-activity-designers.md)   
 [Atraso](../workflow-designer/delay-activity-designer.md)   
 [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)   
 [WriteLine](../workflow-designer/writeline-activity-designer.md)