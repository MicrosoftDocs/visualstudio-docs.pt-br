---
title: Simplificar a expressão LINQ
description: Essa refatoração é usada para remover chamadas desnecessárias para o Enumerable para o método Where.
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 20a3524d786b1f03fc3e221d1b257892d9439a0b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466161"
---
# <a name="simplify-linq-expression"></a>Simplificar a expressão LINQ

Esta refatoração aplica-se a:

- C#

**O que:** Refactores instâncias de `SomeEnumerableType.Where(<LambdaExpression>).Single()` para `SomeEnumerable.Single(<LambdaExpression>)` , `Enumerable.Single()` bem como os seguintes métodos enumeráveis:,,,,, `SingleOrDefault()` `Last()` `LastOrDefault()` `Any()` `Count()` `First()` e `FirstOrDefault()` .

**Quando:**  Todas as instâncias em que o método chama `Single()` , `SingleOrDefault()` e assim por diante, não têm nenhum argumento e são precedidas por uma `Where()` expressão. A entrada para a `Where()` expressão não pode ser construída como uma árvore de expressão.

**Por que:** Remover a chamada desnecessária para o Enumerable para o `.Where()` método melhora o desempenho e a legibilidade.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor dentro da `SomeEnumerableType.Where(<LambdaExpression>).Single()` instância no Visual Studio.
2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.
3. Selecione **simplificar expressão LINQ**

   ![Converter typeof em nameof](media/simplify-linq-expression.png)

## <a name="see-also"></a>Confira também

- [Refatoração](../refactoring-in-visual-studio.md)
