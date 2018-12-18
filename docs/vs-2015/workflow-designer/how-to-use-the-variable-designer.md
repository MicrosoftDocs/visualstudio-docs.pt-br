---
title: 'Como: usar o Designer variável | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 2348fbe0ed51f72ee1218f7ed1ed2006a48a124d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49265103"
---
# <a name="how-to-use-the-variable-designer"></a>Como: Use o designer variável
O designer variável é usado para criar variáveis para uso em cenários e em instruções condicionais de associação de dados. O designer é acessado clicando o **variáveis** botão no canto inferior esquerdo da tela de design. O designer contém uma lista de variáveis que aparecem em um formulário tabular e podem ser classificados por cada um dos cabeçalhos de coluna, exceto para o **padrão** coluna. Cada variável contém um nome, um tipo de variável, um escopo, e um valor padrão (se houver). O nome e o valor padrão são campos editáveis de texto, e o tipo e escopo são gota- suspensa. O escopo é a atividade que foi selecionada quando o designer variável foi chamado. Se uma variável não pode ser criado no escopo de seleção, então o escopo usará padrão a atividade a mais próxima de ancestral de seleção que permite variáveis criado em seu escopo. [!INCLUDE[crabout](../includes/crabout-md.md)] variáveis, consulte [variáveis e argumentos](http://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8).  
  
 A ordem de classificação não é aplicado até que o usuário explicitamente use um dos controles de classificação, feche e reabra o designer variável, ou cria outra variável.  
  
### <a name="to-create-a-new-variable"></a>Para criar uma nova variável  
  
1.  Abra uma solução de fluxo de trabalho ou de atividade em [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
2.  Na tela de design, selecione uma atividade no fluxo de trabalho.  
  
3.  Abra o designer variável clicando o **variáveis** botão no canto inferior esquerdo da tela de design. O designer variável aparece.  
  
4.  Clique na linha vazia rotulada **criar variável**. Isso adicionará uma nova linha com uma nova variável usando os seguintes valores padrão: variablex para o **nome** onde x é um inteiro com um valor inicial de 1, que é incrementado automaticamente para criar nomes de variável exclusivos,  **Cadeia de caracteres** para o **tipo de variável**, e **sequência** para o **escopo**. Nenhum valor é adicionado para **padrão**. Você pode alterar esses valores a qualquer momento durante o processo de design de fluxo de trabalho.  
  
    > [!NOTE]
    >  Para excluir uma variável, selecione a variável clicando nele e, em seguida, pressione a **excluir** chave.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Designer de fluxo de trabalho](../workflow-designer/using-the-workflow-designer.md)   
 [Variáveis e argumentos](http://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8)   
 [Como usar o designer de argumento](../workflow-designer/how-to-use-the-argument-designer.md)