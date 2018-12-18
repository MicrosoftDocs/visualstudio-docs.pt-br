---
title: Caixa de diálogo Editor de condição de regra (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleConditionDialog.UI
helpviewer_keywords:
- Rule Condition dialog box
ms.assetid: c7ca8be9-de31-4a64-939c-4d53a50d5e29
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 0503f6ca9a209c62f842c9428cf1af9fe2a07ccc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49838537"
---
# <a name="rule-condition-editor-dialog-box-legacy"></a>Regra a caixa de diálogo editor de condição (o legados)
Este tópico descreve como usar o **Rule Condition Editor** caixa de diálogo em novas [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Criar e modificar condições declarativas de regra usando o **Rule Condition Editor** caixa de diálogo. Essas condições de regras são expostas como propriedades nas seguintes atividades de para fora da caixa do Windows Workflow Foundation:  
  
- [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)  
  
- [IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)  
  
- [ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)  
  
- [WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)  
  
- [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040)  
  
- [StateMachineWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65045)  
  
  Você acessa o **Rule Condition Editor** caixa de diálogo usando o [selecione a caixa de diálogo condição (herdado)](../workflow-designer/select-condition-dialog-box-legacy.md).  
  
  A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **Rule Condition Editor** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Condição:**|Insira a expressão para a condição de regra.|  
|**OK**|Clique para salvar a condição de regra.|  
  
## <a name="entering-condition-expressions"></a>Inserindo expressões de condição  
 Expressões de condição estão inseridos como texto. Você pode digitar **isso.** no editor para fazer referência a campos, propriedades e métodos usados no fluxo de trabalho, usando um menu do tipo IntelliSense. Ou você pode digitar um nome de membro de fluxo de trabalho diretamente. Você pode adicionar operadores lógicos a condição, como AND, OU, e NOT. Você também pode adicionar predicados. Um predicado é um operador binário e dois operandos. Os operadores binários suportados são **==**, **>**, **\<**, **>=**, e **<=**. Os operandos são suportados valor constante, função aritmética, e membros públicos o escopo.  
  
 Você pode especificar o tipo de comparação, e você pode comparar com **nulo** ou uma cadeia de caracteres vazia. Você pode fazer chamadas aninhados aos membros em uma variável que contém um tipo complexo, por exemplo, `this.Address.State == "WA"`.  
  
 O editor de condição de regra oferece suporte aos seguintes operadores:  
  
- Operadores relacionais: ==, =! =  
  
- Operadores de comparação: <, \<=, >, > =  
  
- Operadores aritméticos: +, -, *,/, MODIFICAÇÃO  
  
- Operadores lógicos: E, & &, OR, &#124; &#124;, não!  
  
- Operadores bit a bit: &,&#124;  
  
  Precedência de operadores de expressão segue regras de precedência de operador C#.  
  
  O editor de condição de regra suporta as seguintes expressões numéricas:  
  
  == 1D de this.i (resoluções a 1,0)  
  
  == 1E1 de this.i (resoluções a 10,0)  
  
  == 1L de this.i (resoluções como um longo)  
  
  == 1M de this.i (resoluções como um decimal)  
  
  == 1F de this.i (resoluções como um único)  
  
  == 1U de this.i (resoluções como um unsigned int)  
  
  Para obter mais informações sobre as condições, consulte [usando condições em fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65009).  
  
## <a name="see-also"></a>Consulte também  
 [IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)   
 [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)   
 [ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)   
 [WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)   
 [Selecione a caixa de diálogo condição (herdado)](../workflow-designer/select-condition-dialog-box-legacy.md)   
 [Usando condições em fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65009)   
 [Designer herdado para a ajuda da interface do usuário do Windows Workflow Foundation](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)