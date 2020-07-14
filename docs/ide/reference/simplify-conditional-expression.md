---
title: Simplificar expressão condicional
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d0571c01217441d4a39fbfe6fb58ccfe95fd0c5a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290049"
---
# <a name="simplify-conditional-expression-refactoring"></a>Simplificar a refatoração de expressão condicional

Esta refatoração aplica-se a:

- C#

**O que:** Permite simplificar uma [expressão condicional](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).

**Quando:** Você deseja remover o código desnecessário para fornecer mais clareza.

**Por que:** Simplificar uma expressão condicional pode fornecer mais clareza e sintaxe concisa. Essa ferramenta de refatoração executará a tarefa automaticamente em vez de fazer isso manualmente.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor na expressão condicional:

2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

3. Selecione **simplificar expressão condicional**

    ![Simplificar expressão condicional](media/simplify-conditional-expression.png)

## <a name="see-also"></a>Veja também

- [Refatoração](../refactoring-in-visual-studio.md)