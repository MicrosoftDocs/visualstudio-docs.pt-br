---
title: Designer de atividade Pick | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: f0a3d5487d60a796f8bf9727c07df1afc959de5c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49221514"
---
# <a name="pick-activity-designer"></a>Escolha o designer de atividades
A atividade de <xref:System.Activities.Statements.Pick> fornece o fluxo de controle baseado. A atividade executa um dos vários ramificações em resposta a um evento disparando.  
  
## <a name="the-pick-activity"></a>A atividade de picareta  
 Uma atividade de <xref:System.Activities.Statements.Pick> contém uma coleção de objetos <xref:System.Activities.Statements.PickBranch> , uma que a atividade de <xref:System.Activities.Statements.Pick> pode executar devido a qualquer evento de entrada que serve como um disparador. Dessa forma [!INCLUDE[wfd1](../includes/wfd1-md.md)] fornece a modelagem com base em eventos de fluxo de controle. Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A>. No início da execução de uma atividade de <xref:System.Activities.Statements.Pick> , todas as atividades do disparador de elementos de <xref:System.Activities.Statements.PickBranch> são agendadas. Quando a primeira atividade concluir, a atividade correspondente de ação está agendada, e quaisquer atividades restantes do disparador serão canceladas.  
  
### <a name="how-to-use-the-pick-activity-designer"></a>Como usar o designer de atividade de picareta  
 O **escolher** designer de atividade pode ser encontrado na **fluxo de controle** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **escolher** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que os designers de atividade são colocados normalmente, por exemplo, dentro de um  **Sequência** designer de atividade. Após solto na [!INCLUDE[wfd2](../includes/wfd2-md.md)], cria uma atividade de <xref:System.Activities.Statements.Pick> , que contém por padrão duas atividades vazios de <xref:System.Activities.Statements.PickBranch> como elementos com nomes para exibição de Branch1 e de Branch2. Esses respectivos <xref:System.Activities.Statements.PickBranch.DisplayName%2A> valores de propriedade podem ser editados na **PickBranch** cabeçalho do designer de atividade ou dentro de **propriedades** janela para cada ramificação.  
  
 Há duas maneiras de adicionar <xref:System.Activities.Statements.PickBranch> atividades para a coleção de um <xref:System.Activities.Statements.Pick> objeto: arrastando e soltando o **PickBranch** designer dos **caixa de ferramentas** ou usando o menu de contexto do dentro de **escolher** superfície de design. Para obter detalhes, consulte o [PickBranch](../workflow-designer/pickbranch-activity-designer.md) tópico. Observe que o único item que pode ser colocado dentro de um **escolher** designer de atividade é um **PickBranch** designer de atividade.  
  
### <a name="pick-activity-properties-in-the-workflow-designer"></a>Escolha propriedades de atividade em Designer de Fluxo de Trabalho  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Pick> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável do designer de atividade de <xref:System.Activities.Statements.Pick> no cabeçalho. O valor padrão é picareta. O valor pode ser editado na grade de propriedade ou diretamente no cabeçalho do designer de atividade.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de controle](../workflow-designer/control-flow-activity-designers.md)   
 [Escolher atividade](http://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)   
 [Usando a atividade de Pick](http://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)