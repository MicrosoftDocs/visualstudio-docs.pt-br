---
title: Converter um loop foreach em LINQ
description: Converta qualquer loop foreach que use um IEnumerable para uma consulta LINQ ou um formulário de chamada LINQ (também conhecido como um método LINQ).
ms.date: 07/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 8ff489e11cc5c61c5e840b4b12d05ba5da46ce41
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466284"
---
# <a name="convert-a-foreach-loop-to-linq"></a>Converter um loop foreach em LINQ

Esta refatoração aplica-se a:

- C#

**O que:** Permite que você converta facilmente seu loop *foreach* que usa um IEnumerable para uma consulta LINQ ou um formulário de chamada LINQ (também conhecido como um método LINQ).

**Quando:** Você tem um loop foreach que usa um IEnumerable e deseja que esse loop seja lido como uma consulta LINQ.

**Por que:** Você prefere usar a sintaxe LINQ em vez de um loop foreach. O [LINQ](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq) faz uma consulta em um constructo de linguagem de primeira classe no C#. O LINQ pode reduzir a quantidade de código em um arquivo, facilitar a leitura e permitir que diferentes fontes de dados tenham padrões de expressão de consulta semelhantes.

> [!NOTE]
> A sintaxe LINQ é normalmente menos eficiente do que um loop foreach. É bom estar ciente de que pode ocorrer alguma compensação de desempenho ao usar o LINQ para melhorar a legibilidade do código.

## <a name="convert-a-foreach-loop-to-linq-refactoring"></a>Converter um loop foreach em refatoração de LINQ

1. Coloque o cursor na palavra-chave `foreach`.

    ![Exemplo de foreach com IEnumerable](media/convert-foreach-to-LINQ.png)

2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

   ![Converter em um exemplo de menu LINQ](media/convert-foreach-to-LINQ-codefix.png)

3. Selecione **Converter em LINQ** ou **Converter em Linq (formulário de chamada)**.

   ![Exemplo de resultado da consulta LINQ](media/convert-foreach-to-LINQ-result.png)

   ![Exemplo de resultado do formulário de chamada LINQ](media/convert-foreach-to-LINQ-callform-result.png)

### <a name="sample-code"></a>Código de exemplo

```csharp
using System.Collections.Generic;

public class Class1
{
    public void MyMethod()
    {
        var greetings = new List<string>()
            { "hi", "yo", "hello", "howdy" };

        IEnumerable<string> enumerable()
        {
            foreach (var greet in greetings)
            {
                if (greet.Length < 3)
                {
                    yield return greet;
                }
            }

            yield break;
        }
    }
}
```

## <a name="see-also"></a>Confira também

- [Refatoração](../refactoring-in-visual-studio.md)
- [Janela Visualização de Alterações](../../ide/preview-changes.md)
- [Dicas para desenvolvedores do .NET](../csharp-developer-productivity.md)
