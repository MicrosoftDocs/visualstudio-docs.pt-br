---
title: Designer de atividade de PickBranch | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: f39479c9421ab87caf7c918e05be89272f0fb4de
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887291"
---
# <a name="pickbranch-activity-designer"></a>Designer de atividade de PickBranch
<xref:System.Activities.Statements.PickBranch> fornece um caminho de execução baseado em uma atividade de <xref:System.Activities.Statements.Pick> que pode ser acionada por um evento de entrada.  
  
## <a name="pickbranch"></a>PickBranch  
 os objetos de<xref:System.Activities.Statements.PickBranch> estão contidos na coleção de <xref:System.Activities.Statements.Pick.Branches%2A> de uma atividade de <xref:System.Activities.Statements.Pick> . Cada <xref:System.Activities.Statements.PickBranch> está contido em uma ramificação de atividade de <xref:System.Activities.Statements.Pick> e pode ser executado devido a qualquer evento de entrada que serve como um disparador. Dessa forma [!INCLUDE[wfd1](../includes/wfd1-md.md)] fornece a modelagem com base em eventos de fluxo de controle. Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A>.  
  
### <a name="how-to-use-the-pick-activity-designer"></a>Como usar o designer de atividade de picareta  
 O **PickBranch** designer pode ser encontrada na **fluxo de controle** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas** guia [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** da **exibição** menu, ou CTRL + ALT + X).  
  
 Dois vazio <xref:System.Activities.Statements.PickBranch> objetos com nomes para exibição de **Branch1** e **Branch2** são criados por padrão como elementos de um <xref:System.Activities.Statements.Pick> atividade quando o **escolher** designer de atividade é solto inicialmente sobre o [!INCLUDE[wfd2](../includes/wfd2-md.md)]. Esses respectivos <xref:System.Activities.Statements.PickBranch.DisplayName%2A> valores de propriedade podem ser editados na **PickBranch** cabeçalho do designer ou dentro de **propriedades** janela para cada ramificação.  
  
 Há duas maneiras de adicionar <xref:System.Activities.Statements.PickBranch> objetos à coleção de um <xref:System.Activities.Statements.Pick> objeto: arrastando e soltando o **PickBranch** designer dos **caixa de ferramentas** ou usando o menu de contexto do dentro de **escolher** superfície de design:  
  
1. O **PickBranch** designer cria um <xref:System.Activities.Statements.PickBranch> quando ele é arrastado dos **caixa de ferramentas** e solto em um dos ramificações de um **escolher** designer de atividade no [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície. Novos objetos de <xref:System.Activities.Statements.PickBranch> podem ser colocados dentro do designer de <xref:System.Activities.Statements.Pick> para a esquerda ou direita de todos os elementos existentes de <xref:System.Activities.Statements.PickBranch> já contidos na coleção. Ao arrastar uma **PickBranch** designer para o **escolher** designer com o mouse, o **escolher** designer usa uma faixa azul cinza vertical para indicar onde o <xref:System.Activities.Statements.PickBranch> é adicionado para um determinada posicionamento do mouse.  
  
2. Clique com botão direito **escolher** designer de atividade (mas não estão dentro **PickBranch** designer) para obter um menu de contexto e selecione **criar ramificação** para adicionar um novo <xref:System.Activities.Statements.PickBranch>. Observe que o novo <xref:System.Activities.Statements.PickBranch> é adicionada à direita da existente <xref:System.Activities.Statements.PickBranch> objetos na **escolher** designer.  
  
   O **PickBranch** designer pode ser expandido para revelar as **gatilho** e **ação** caixas ou recolhidos clicando-se os sinais de interpolação duplas no lado direito dos cabeçalhos. Editar o <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A> de cada <xref:System.Activities.Statements.PickBranch> soltando atividades na **gatilho** e **ação** caixas de seus designers.  
  
   O <xref:System.Activities.Statements.PickBranch> objetos na <xref:System.Activities.Statements.Pick.Branches%2A> coleção de uma <xref:System.Activities.Statements.Pick> de objeto, podem ser reordenadas arrastando e soltando-os para um novo local dentro de **escolher** designer. O **escolher** designer usa uma faixa azul cinza vertical para indicar onde o <xref:System.Activities.Statements.PickBranch> é adicionado para um determinada posicionamento do mouse.  
  
   Há duas maneiras para excluir <xref:System.Activities.Statements.PickBranch>:  
  
3. Selecione o **PickBranch** designer e excluí-lo.  
  
4. Selecione o **PickBranch** designer, clique com botão direito para obter o menu de contexto e selecione **excluir**.  
  
   Certifique-se de selecionar o **PickBranch** designer, como selecionar uma das atividades dentro de seu **gatilho** ou **ação** encaixota exclui por engano uma dessas atividades e não o <xref:System.Activities.Statements.PickBranch> objeto.  
  
### <a name="pickbranch-properties-in-the-workflow-designer"></a>Propriedades de PickBranch em Designer de Fluxo de Trabalho  
 A tabela a seguir mostra as propriedades mais úteis de <xref:System.Activities.Statements.PickBranch> e descreve como usá-los em [!INCLUDE[wfd2](../includes/wfd2-md.md)].  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|False|O nome amigável exibido no cabeçalho do **PickBranch** designer. O valor padrão é ramificação.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|verdadeiro|Cada <xref:System.Activities.Statements.PickBranch> contém uma ação de <xref:System.Activities.Statements.PickBranch.Trigger%2A> que pode chamar <xref:System.Activities.Statements.PickBranch.Action%2A>.|  
|<xref:System.Activities.Statements.PickBranch.Action%2A>|False|Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Action%2A> que é executado se disparado.|  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de controle](../workflow-designer/control-flow-activity-designers.md)   
 [Escolher atividade](http://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)   
 [Usando a atividade de Pick](http://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)