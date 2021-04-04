---
title: Usar new()
description: Saiba como usar o `new()` quando não for possível usar o `var` .
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 889be18ab342f515bf5add266088a7ee69c087c1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218068"
---
# <a name="use-new"></a>Use `new()`.

Isso se aplica a:

- C#

**O que:** Use o `new()` .

**Quando:** Você tem um campo que não pode usar `var` ou uma preferência de estilo de código para não usar `var` .

**Por que:** Portanto, você não precisa escrever código repetitivo repetindo o tipo duas vezes.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor na declaração de campo.

2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

3. Selecione **usar ' novo (...) '**:

    ![Usar ' New (...) '](media/use-new.png)

## <a name="see-also"></a>Confira também

- [Refatoração](../refactoring-in-visual-studio.md)
