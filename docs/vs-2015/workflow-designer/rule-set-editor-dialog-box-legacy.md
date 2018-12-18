---
title: (Herdado) caixa de diálogo Editor de conjunto de regras | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleSetDialog.UI
helpviewer_keywords:
- Rule Set Editor dialog box
ms.assetid: 7cfd5df1-1115-4e5c-9b72-121f39419e83
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 3469e395ee50e63f8ac76e4181d02b777ccbd4ba
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942394"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>Caixa de diálogo do editor de regra (legados)
Este tópico descreve como usar o **Rule Set Editor** caixa de diálogo em novas [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 O **Rule Set Editor** caixa de diálogo é usada para criar e modificar [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019) conjuntos de regra, que são serializados em um arquivo. rules.  
  
> [!NOTE]
>  Se você quiser abrir o arquivo. Rules com o **Editor de XML com codificação**, primeiro você deve fechar a janela de designer associado para o fluxo de trabalho ou atividade.  
  
 Para obter informações sobre como acessar o **Rule Set Editor** caixa de diálogo, consulte [como: criar um PolicyActivity do conjunto de regras (herdado)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md).  
  
> [!WARNING]
>  O editor das regras de novas [!INCLUDE[wfd2](../includes/wfd2-md.md)] que é usado para direcionar [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] não oferece suporte Multitargeting.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **Rule Set Editor** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Adicionar regra**|Adicione uma nova definição de regra ao conjunto de regras.|  
|**Excluir**|Exclui a regra selecionada do conjunto de regras.|  
|**O encadeamento**|Especifica que tipo de encadeamento frente para usar com o conjunto de regras. As opções disponíveis são:<br /><br /> -   **Total de encadeamento**, que especifica usar todos mecanismos encadeando dianteiros: método implícito, atribuindo e explícito usando uma **atualização** função.<br />-   **Sequencial**, que especifica para não usar qualquer encadeamento frente.<br />-   **Atualização explícita apenas&lt;1**, que especifica para executar somente encadeamento frente na **atualização** ações.<br /><br /> Para obter mais informações sobre o encadeamento, consulte [usando a atividade de PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65004).|  
|**Nome**|Regra título da coluna da lista. Clique para classificar por nome a lista de regras.|  
|**prioridade**|Regra título da coluna da lista. Clique para classificar a lista de regras por prioridade.|  
|**Reavaliação**|Regra título da coluna da lista. Clique para classificar a lista de regras pelo tipo de reavaliação.|  
|**Visualização de regra**|Regra título da coluna da lista. Clique para classificar a lista de regras por visualização de condição e ações de uma regra.|  
|**Nome:**|Digite o nome da regra.|  
|**Prioridade:**|Insira uma prioridade para a regra. A prioridade padrão é 0.|  
|**Reavaliação:**|Especifica que tipo de reavaliação de regras para usar com a regra. As opções disponíveis são:<br /><br /> -   **Sempre**, que faz com que a regra ser reavaliada conforme necessário.<br />-   **Nunca**, que faz com que a regra ser reavaliada nunca. Neste caso uma regra executa somente uma vez.|  
|**Active Directory**|Verifique para fazer a regra ativo.|  
|**Condição:**|Digite uma expressão para a condição de regra. Para obter informações sobre a sintaxe de expressão, consulte a seção “inserindo de expressões de condição e a ação” nessa página.|  
|**Ações:**|Insira a expressão para ações. Para obter informações sobre a sintaxe de expressão, consulte a seção “inserindo de expressões de condição e a ação” nessa página.|  
|**Outras ações:**|Insira a expressão para outras ações. Para obter informações sobre a sintaxe de expressão, consulte a seção “inserindo de expressões de condição e a ação” nessa página.|  
|**OK**|Clique para salvar a regra definida como um arquivo de .rules.|  
  
 Para obter mais informações sobre conjuntos de regras, consulte [usando a atividade de PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65004).  
  
## <a name="entering-condition-and-action-expressions"></a>Inserindo expressões de condição e de ação  
 Você inserir expressões para a condição e Then e Else ações como texto em seu respectivo texto nas caixas de **Rule Set Editor** caixa de diálogo. Você pode digitar **isso.** no editor para fazer referência a campos, propriedades e métodos usados no fluxo de trabalho, usando um IntelliSense-tipo de menu. Ou você pode digitar um nome de membro de fluxo de trabalho diretamente. Você pode chamar métodos estáticos em tipos referenciados digitando o nome da classe seguida do nome do método.  
  
 Você pode adicionar operadores lógicos a condição, como AND, OU, e NOT. Você também pode adicionar predicados. Um predicado é um operador binário e dois operandos. Os operadores binários suportados são = =, >, \<, > =, e < =. Os operandos são suportados valor constante, função aritmética, e membros públicos o escopo.  
  
 Você pode especificar o tipo de comparação, e você pode comparar com **nulo** ou uma cadeia de caracteres vazia. Você pode aninhar chamadas aos membros em uma variável que contém um tipo complexo, por exemplo, `this.Address.State == "WA"`.  
  
 As expressões dão suporte aos seguintes operadores:  
  
- Operadores relacionais: ==, =! =  
  
- Operadores de comparação: <, \<=, >, > =  
  
- Operadores aritméticos: +, -, *,/, MODIFICAÇÃO  
  
- Operadores lógicos: E, & &, OR, &#124; &#124;, não!  
  
- Operadores bit a bit: &,&#124;  
  
  Precedência de operadores de expressão segue regras de precedência de operador C#.  
  
  Para obter mais informações sobre as condições, consulte [usando condições em fluxos de trabalho](http://msdn.microsoft.com/en-us/541211f5-d382-4810-894f-71f00b34fa77).  
  
### <a name="halt-and-update-functions"></a>Interromper e atualizar funções  
 **Ações:** e **ações Else:** dar suporte a expressões **interromper** e **atualização** funções. Para usar o **Halt** de função, digite **interromper** em um **, em seguida, a ação:** ou **outra ação:** caixa de texto. O **Halt** ação faz com que a regra a execução de parar imediatamente, e o controle retorna para o código de chamada. Você usa o **atualização** função com o encadeamento de encaminhamento.  
  
 Uma **atualização** instrução pode ser expressa no editor em um dos dois formulários; ambos os formatos são mostrados no exemplo a seguir:  
  
```  
Update(this.Address.State)  
Update("this/Address/State")  
```  
  
 Para obter mais informações sobre como usar **atualização** com o encadeamento de encaminhamento, consulte [usando a atividade de PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65004).  
  
## <a name="see-also"></a>Consulte também  
 [PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)   
 [Caixa de diálogo Definir selecione regra (herdado)](../workflow-designer/select-rule-set-dialog-box-legacy.md)   
 [Usando a atividade de PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65004)   
 [Usando condições em fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65009)