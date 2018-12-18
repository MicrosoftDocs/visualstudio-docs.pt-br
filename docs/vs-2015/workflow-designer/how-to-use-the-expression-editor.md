---
title: 'Como: usar o Editor de expressões | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 0c41de63b4163f1fd259ffa4adcef63cad92e351
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49181708"
---
# <a name="how-to-use-the-expression-editor"></a>Como: Use o editor de expressão
O editor de expressão é um controle de [!INCLUDE[wfd1](../includes/wfd1-md.md)] que é usado em muitas atividades de fluxo de trabalho como um meio de inserir e avaliar dessas expressões. O editor de expressão fornece IDE completo que a experiência de edição IntelliSense, que inclui coloração, ParamInfo, squiggles de erro, entre outros recursos. O compilador valida a expressão após está conectado. Se a expressão é inválido, um ícone de erro é exibido. O editor também pode ser aberto como uma **Editor de expressão** caixa de diálogo.  
  
 As expressões são valores ou código literal de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] associado aos argumentos ou propriedades. Eles contêm elementos de valor (por exemplo, variáveis, constantes, literais, propriedades) que são combinados com operações para produzir um novo valor. As expressões são escritas usando a sintaxe de VB.NET mesmo se o aplicativo estiver em um programa usando C#. Isso significa que a maiusculas não importa, a comparação é realizada usando uma única é igual a entrada ("=") em vez de ("= ="), os operadores boolianos são as palavras "e" e "ou" em vez dos símbolos "& &" e "&#124;&#124;", e **nada**  é usado em vez de **nulo**. Para obter mais informações sobre expressões e operadores no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e para alguns exemplos, consulte [operadores e expressões no Visual Basic](http://go.microsoft.com/fwlink/?LinkId=186818).  
  
 O **Editor de expressão** se comporta da seguinte maneira:  
  
-   Se o foco não estiver no editor de expressão, parece um controle normal TextBlock.  
  
-   Uma vez que o foco estiver no editor de expressão, e ele se comporta como o controle editor de expressão. Após perde o foco, parece uma TextBlock normal novamente.  
  
-   Se você fica no editor de expressão em um designer rehosted de fluxo de trabalho, então se comporta como uma caixa de texto. Quando o foco é perdido no designer rehosted de fluxo de trabalho, o editor de expressão parece uma TextBlock normal novamente.  
  
> [!NOTE]
>  O IntelliSense para o editor de expressão está disponível somente dentro de [!INCLUDE[vs2010](../includes/vs2010-md.md)]. Em [!INCLUDE[vs2010](../includes/vs2010-md.md)] e em cenários rehosted, o compilador valida a expressão após está conectado e o editor de expressão um ícone de erro se a expressão não é válido.  
  
### <a name="using-the-expression-editor"></a>Usando o editor de expressão  
  
1.  Em [!INCLUDE[vs2010](../includes/vs2010-md.md)], abra um projeto novo ou existente de fluxo de trabalho.  
  
2.  Adicione, por exemplo, a atividade de <xref:System.Activities.Statements.Assign> ao fluxo de trabalho.  
  
    > [!NOTE]
    >  Várias atividades de fluxo de trabalho têm editores de expressão. A expressão TextBlocks também aparece no designer variável, no designer do argumento, e no designer dinâmico do argumento. A atividade de <xref:System.Activities.Statements.Assign> é usada como um exemplo.  
  
3.  Clique no editor de expressão esquerdo do designer de atividade para atividades de <xref:System.Activities.Statements.Assign> .  
  
     As cadeias de caracteres de marca d'água cinza  **\<para >** e  **\<insira uma expressão VB >** são o padrão de cadeias de caracteres de texto para editores de expressão no <xref:System.Activities.Statements.Assign> atividade.  
  
4.  Digite sua expressão. Se você inserir uma cadeia de caracteres, certifique-se coloque aspas ao redor de cadeia de caracteres. Se você escolher para associar o argumento da expressão a uma variável, deixe a aspas - tica.  
  
     Quando você terminar, selecione uma região ou uma área fora do editor de expressão para deslocar o foco a outra parte do designer. Isso fará com que o compilador validar a expressão como descrito anteriormente.  
  
     Entrada de maneira alternativa/edição uma expressão é clique nas reticências ao lado do nome da propriedade na grade de propriedade. Isso abrirá o **Editor de expressão** como caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Activities.Presentation.View.ExpressionTextBox>