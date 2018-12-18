---
title: 'Como: criar uma condição de regra declarativa (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- declarative rule conditions
- condition statements, declarative rule conditions
- Rule Condition Editor dialog box
ms.assetid: 804b6129-c433-408f-a424-46987967730c
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 2508404840db81f03ba4865a3e5d5af91e5c653b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49187402"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>Como: Crie uma condição declarativa de regra (o legados)
Este tópico descreve como declarar uma condição de regra usando o novas [!INCLUDE[wfd1](../includes/wfd1-md.md)] que direciona [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Uma instrução de condição é avaliada como **verdadeira** ou **falso**. Uma condição de regra declarativa é uma instrução de condição que é criada usando o [caixa de diálogo de Editor de condição de regra (herdado)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md) e armazenados como XML com o fluxo de trabalho. Pode incluir os predicados que comparam o estado de fluxo de trabalho e a algebra booleano que combina vários predicados.  
  
 As condições declarativas de regras são usadas nas seguintes atividades de para fora da caixa do Windows Workflow Foundation:  
  
-   [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)  
  
-   [IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)  
  
-   [ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)  
  
-   [WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)  
  
-   [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040)  
  
-   [StateMachineWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65045)  
  
### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>Para criar uma condição de regra declarativamente usando o editor de condição de regra  
  
1.  Na atividade de **propriedades** janela, clique no **condição** propriedade ou **UntilCondition** propriedade, dependendo da atividade.  
  
2.  Selecione **condição de regra declarativa** na lista para a propriedade.  
  
3.  Expanda o **condição** ou **UntilCondition** propriedade.  
  
4.  Clique o **ConditionName** propriedade.  
  
5.  Clique o **ConditionName** elipses **[...]**  para abrir o **Selecionar condição** caixa de diálogo.  
  
6.  Clique em **nova condição** para abrir o **Editor de condição de regra** caixa de diálogo.  
  
7.  Digite a expressão para a condição na **condição** caixa de texto.  
  
     Para obter informações sobre como criar expressões de condição, consulte [caixa de diálogo de Editor de condição de regra (herdado)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md).  
  
8.  Quando tiver terminado de criar a expressão de condição, clique em **Okey** para fechar a caixa de diálogo e criar a condição de regra com um nome atribuído.  
  
     O **Selecionar condição** caixa de diálogo é aberta.  
  
     Para obter informações sobre como usar o **Selecionar condição** caixa de diálogo, consulte [selecione a caixa de diálogo condição (herdado)](../workflow-designer/select-condition-dialog-box-legacy.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atividades de fluxo de trabalho herdado](../workflow-designer/legacy-workflow-activities.md)   
 [Usando o ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65066)   
 [Usando a atividade de IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65075)   
 [Usando a atividade Replicator](http://go.microsoft.com/fwlink?LinkID=65080)   
 [Usando While atividade](http://go.microsoft.com/fwlink?LinkID=65091)   
 [Caixa de diálogo Editor de condição de regra (herdado)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)   
 [Selecione a caixa de diálogo condição (herdado)](../workflow-designer/select-condition-dialog-box-legacy.md)   
 [Usando condições em fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65009)