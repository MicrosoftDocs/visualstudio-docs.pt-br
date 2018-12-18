---
title: Atrasar o Designer de atividade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: b861eb70315b2a734cdedb4346e0bcd9f2143678
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49282757"
---
# <a name="delay-activity-designer"></a>Atrasar o designer de atividades
O **atraso** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Delay> atividade.  
  
## <a name="the-delay-activity"></a>A atividade do atraso  
 A atividade de <xref:System.Activities.Statements.Delay> atrasa a execução de um fluxo de trabalho para uma quantidade de tempo especificada.  
  
### <a name="using-the-delay-activity-designer"></a>Usando o designer de atividade do atraso  
 O **atraso** designer de atividade pode ser encontrado na **primitivos** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CTRL + ALT + X.)  
  
 O **atraso** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.Delay> com uma opção <xref:System.Activities.Activity.DisplayName%2A> de atraso. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **atraso** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-delay-properties"></a>As propriedades do atraso  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Delay> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns deless podem ser editados na superfície do designer de [!INCLUDE[wfd2](../includes/wfd2-md.md)].  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Delay> . O padrão é atraso. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.Delay.Duration%2A>|verdadeiro|A quantidade de tempo para atrasar o fluxo de trabalho. Essa propriedade é definida na grade de propriedade. Digite qualquer um <xref:System.TimeSpan> literal no 00:00 de formato: 00 ou uma expressão do Visual Basic para especificar a quantidade de tempo.|  
  
## <a name="see-also"></a>Consulte também  
 [Primitivos](../workflow-designer/primitives-activity-designers.md)   
 [Atribuir](../workflow-designer/assign-activity-designer.md)   
 [Designer de atividade de atraso](../workflow-designer/delay-activity-designer.md)   
 [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)   
 [WriteLine](../workflow-designer/writeline-activity-designer.md)