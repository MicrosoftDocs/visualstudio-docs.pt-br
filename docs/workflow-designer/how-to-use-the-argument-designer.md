---
title: 'Designer de fluxo de trabalho - como: usar o Designer de argumento'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 868fc13474e90be219cf1acebc00074641df142e
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36755516"
---
# <a name="how-to-use-the-argument-designer"></a>Como: Use o designer do argumento

Em comparação com versões anteriores do .NET Framework, o designer do argumento facilita permitir que os dados e fluam fora de uma atividade. O designer é acessado clicando o **argumentos** botão no canto inferior esquerdo da tela de design. O designer contém uma lista de argumentos que aparecem em um formulário tabular e podem ser classificados por cada um dos cabeçalhos de coluna, exceto para o **valor padrão** coluna. Cada argumento contiver um nome, a direção de in/out/in-out/property, o tipo, e o valor padrão de expressão (se houver). O nome e o valor padrão de expressão são campos editáveis de texto, e o tipo e direção são gota- suspensa. Para obter mais informações, consulte [variáveis e argumentos (.NET)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments).

## <a name="to-create-a-new-argument"></a>Para criar um novo argumento

1.  Abra uma solução de fluxo de trabalho ou atividade no Visual Studio.

2.  Abra o designer dos argumentos clicando o **argumentos** botão no canto inferior esquerdo da tela de design. O designer dos argumentos aparece.

3.  Clique na linha vazia rotulada **argumento criar**. Isso adicionará uma nova linha com um novo argumento usando os seguintes valores padrão: argumentx para o **nome** onde x é um inteiro com um valor inicial de 1, que é incrementado automaticamente para criar nomes exclusivos de argumento, **em**  para o **direção**, e **cadeia de caracteres** para o **tipo de argumento**. Nenhum valor é adicionado para **valor padrão**. Você pode alterar esses valores a qualquer momento durante o processo de design de fluxo de trabalho.

    > [!NOTE]
    > Para excluir um argumento, selecione o argumento clicando nele e, em seguida, pressione a **excluir** chave.

## <a name="see-also"></a>Consulte também

- [Usando o Designer de Fluxo de Trabalho](../workflow-designer/using-the-workflow-designer.md)
- [Variables and Arguments](/dotnet/framework/windows-workflow-foundation/variables-and-arguments) (Variáveis e argumentos)