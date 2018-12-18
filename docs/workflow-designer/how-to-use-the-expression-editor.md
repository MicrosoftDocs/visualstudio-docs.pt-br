---
title: 'Designer de fluxo de trabalho - como: usar o Editor de expressão'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c1f2ab9cad6f54b8d1106fd68eb017434cf5cfef
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36756136"
---
# <a name="how-to-use-the-expression-editor"></a>Como: Use o editor de expressão

O Editor de expressão é um controle de Designer de fluxo de trabalho que é usado em muitas atividades de fluxo de trabalho para inserir e avaliar expressões. O Editor de expressão fornece um IDE completo para edição de experiência, incluindo IntelliSense, coloração, ParamInfo, squiggles de erro, entre outros recursos. O compilador valida a expressão após está conectado. Se a expressão é inválido, um ícone de erro é exibido. O editor também pode ser aberto como uma **Editor de expressão** caixa de diálogo.

As expressões são valores literais ou código do Visual Basic associado aos argumentos ou propriedades. Eles contêm elementos de valor (por exemplo, variáveis, constantes, literais, propriedades) que são combinados com operações para produzir um novo valor. As expressões são escritas usando a sintaxe de VB.NET mesmo se o aplicativo estiver em um programa usando C#. Isso significa que a maiusculas não importa, a comparação é realizada usando um único igual entre ("=" em vez de "= ="), os operadores boolianos são as palavras "e" e "ou" em vez dos símbolos "& &" e "| |", e **nada** é usado em vez de **nulo**. Para obter mais informações sobre expressões e operadores no Visual Basic e para obter alguns exemplos, consulte [operadores e expressões no Visual Basic](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100)).

O **Editor de expressão** se comporta da seguinte maneira:

- Se o foco não estiver no editor de expressão, parece um controle normal TextBlock.

- Uma vez que o foco estiver no editor de expressão, e ele se comporta como o controle editor de expressão. Após perde o foco, o Editor de expressão parece uma TextBlock normal novamente.

- Se você fica no editor de expressão em um designer rehosted de fluxo de trabalho, então se comporta como uma caixa de texto. Quando o foco é perdido no designer rehosted de fluxo de trabalho, o editor de expressão parece uma TextBlock normal novamente.

> [!NOTE]
> IntelliSense para o Editor de expressão está disponível apenas no Visual Studio. No Visual Studio e os cenários rehosted, o compilador valida a expressão após está conectado e o editor de expressão exibe um ícone de erro se a expressão é inválida.

## <a name="use-the-expression-editor"></a>Usar o editor de Expressão

1.  No Visual Studio, abra um projeto de fluxo de trabalho novo ou existente.

2.  Adicione, por exemplo, a atividade de <xref:System.Activities.Statements.Assign> ao fluxo de trabalho.

    > [!NOTE]
    > Várias atividades de fluxo de trabalho têm editores de expressão. A expressão TextBlocks também aparece no designer variável, no designer do argumento, e no designer dinâmico do argumento. A atividade de <xref:System.Activities.Statements.Assign> é usada como um exemplo.

3.  Clique no editor de expressão esquerdo do designer de atividade para atividades de <xref:System.Activities.Statements.Assign> .

     As cadeias de caracteres de marca d'água cinza  **\<para >** e  **\<insira uma expressão VB >** são o padrão de cadeias de caracteres de texto para editores de expressão no <xref:System.Activities.Statements.Assign> atividade.

4.  Digite sua expressão. Se você inserir uma cadeia de caracteres, certifique-se coloque aspas ao redor de cadeia de caracteres. Se você escolher para associar o argumento da expressão a uma variável, deixe a aspas - tica.

     Quando terminar, selecione uma região ou uma área fora do Editor de expressão para deslocar o foco para outra parte do designer. Mudando o foco faz com que o compilador validar a expressão, conforme descrito anteriormente.

     Uma maneira alternativa para inserir ou editar uma expressão é clique nas reticências ao lado do nome da propriedade na grade de propriedade. Selecione as reticências para abrir o **Editor de expressão** como uma caixa de diálogo.

## <a name="see-also"></a>Consulte também

- <xref:System.Activities.Presentation.View.ExpressionTextBox>