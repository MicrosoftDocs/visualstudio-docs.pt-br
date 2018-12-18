---
title: 'Como: usar o Designer de argumento | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 81b24b8c0344cc6a8cf1559126a4faf0bc2b6f4e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49206616"
---
# <a name="how-to-use-the-argument-designer"></a>Como: Use o designer do argumento
Em comparação com versões anteriores de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], o designer do argumento facilita permitir que os dados e fluam fora de uma atividade. O designer é acessado clicando o **argumentos** botão no canto inferior esquerdo da tela de design. O designer contém uma lista de argumentos que aparecem em um formulário tabular e podem ser classificados por cada um dos cabeçalhos de coluna, exceto para o **valor padrão** coluna. Cada argumento contiver um nome, a direção de in/out/in-out/property, o tipo, e o valor padrão de expressão (se houver). O nome e o valor padrão de expressão são campos editáveis de texto, e o tipo e direção são gota- suspensa. [!INCLUDE[crabout](../includes/crabout-md.md)] argumentos, consulte [variáveis e argumentos](http://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8).  
  
### <a name="to-create-a-new-argument"></a>Para criar um novo argumento  
  
1.  Abra uma solução de fluxo de trabalho ou de atividade em [!INCLUDE[vs2010](../includes/vs2010-md.md)].  
  
2.  Abra o designer dos argumentos clicando o **argumentos** botão no canto inferior esquerdo da tela de design. O designer dos argumentos aparece.  
  
3.  Clique na linha vazia rotulada **argumento criar**. Isso adicionará uma nova linha com um novo argumento usando os seguintes valores padrão: argumentx para o **nome** onde x é um inteiro com um valor inicial de 1, que é incrementado automaticamente para criar nomes exclusivos de argumento, **em**  para o **direção**, e **cadeia de caracteres** para o **tipo de argumento**. Nenhum valor é adicionado para **valor padrão**. Você pode alterar esses valores a qualquer momento durante o processo de design de fluxo de trabalho.  
  
    > [!NOTE]
    >  Para excluir um argumento, selecione o argumento clicando nele e, em seguida, pressione a **excluir** chave.  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Designer de fluxo de trabalho](../workflow-designer/using-the-workflow-designer.md)   
 [Variables and Arguments](http://msdn.microsoft.com/library/d03dbe34-5b2e-4f21-8b57-693ee49611b8) (Variáveis e argumentos)