---
title: 'Designer de Fluxo de Trabalho-como: usar o editor de expressão'
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 04c0fdaab87c88028b8c14ca59e93fa93e74be74
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817431"
---
# <a name="how-to-use-the-expression-editor"></a>Como: Use o editor de expressão

O editor de expressão é um controle Designer de Fluxo de Trabalho usado em muitas atividades de fluxo de trabalho para inserir e avaliar expressões. O editor de expressão fornece uma experiência completa de edição de IDE, incluindo IntelliSense, colorização, ParamInfo, rabiscos de erro, entre outros recursos. O compilador valida a expressão depois que ela é inserida. Se a expressão é inválido, um ícone de erro é exibido. O editor também pode ser aberto como uma caixa de diálogo **Editor de expressão** .

As expressões são valores literais ou Visual Basic código associado a argumentos ou propriedades. Eles contêm elementos de valor (por exemplo, variáveis, constantes, literais, Propriedades) que são combinados com operações para gerar um novo valor. As expressões são escritas usando a sintaxe de VB.NET mesmo se o aplicativo estiver em um programa usando C#. Isso significa que a capitalização não importa, a comparação é executada usando um único sinal de igual ("=" em vez de "= ="), os operadores boolianos são as palavras "and" e "or", em vez dos símbolos "&&" e "| |", e **nada** é usado em vez de **NULL**. Para obter mais informações sobre expressões e operadores no Visual Basic e para alguns exemplos, consulte [operadores e expressões em Visual Basic](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100)).

O **Editor de expressões** se comporta da seguinte maneira:

- Se o foco não estiver no editor de expressão, parece um controle normal TextBlock.

- Uma vez que o foco estiver no editor de expressão, e ele se comporta como o controle editor de expressão. Depois de perder o foco, o editor de expressão se parece com um TextBlock regular novamente.

- Se você fica no editor de expressão em um designer rehosted de fluxo de trabalho, então se comporta como uma caixa de texto. Quando o foco é perdido no designer rehosted de fluxo de trabalho, o editor de expressão parece uma TextBlock normal novamente.

> [!NOTE]
> O IntelliSense para o editor de expressão está disponível somente dentro do Visual Studio. No Visual Studio e nos cenários rehospedados, o compilador valida a expressão depois que ela é inserida e o editor de expressão exibe um ícone de erro se a expressão for inválida.

## <a name="use-the-expression-editor"></a>Usar o editor de Expressão

1. No Visual Studio, abra um projeto de fluxo de trabalho novo ou existente.

2. Adicione, por exemplo, a atividade de <xref:System.Activities.Statements.Assign> ao fluxo de trabalho.

    > [!NOTE]
    > Várias atividades de fluxo de trabalho têm editores de expressão. A expressão TextBlocks também aparece no designer variável, no designer do argumento, e no designer dinâmico do argumento. A atividade de <xref:System.Activities.Statements.Assign> é usada como um exemplo.

3. Clique no editor de expressão esquerdo do designer de atividade para atividades de <xref:System.Activities.Statements.Assign> .

     As cadeias de caracteres de marca d' água cinza **\<To>** e **\<Enter a VB Expression>** são as cadeias de caracteres de texto padrão para editores de expressão na <xref:System.Activities.Statements.Assign> atividade.

4. Digite sua expressão. Se você inserir uma cadeia de caracteres, certifique-se coloque aspas ao redor de cadeia de caracteres. Se você escolher para associar o argumento da expressão a uma variável, deixe a aspas - tica.

     Quando terminar, selecione uma região ou área fora do editor de expressão para deslocar o foco para outra parte do designer. A mudança do foco faz com que o compilador valide a expressão conforme descrito anteriormente.

     Uma maneira alternativa de inserir ou editar uma expressão é clicar nas reticências ao lado do nome da propriedade na grade de propriedades. A seleção das reticências abre o **Editor de expressão** como uma caixa de diálogo.

## <a name="see-also"></a>Confira também

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
