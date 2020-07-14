---
title: Conclusão de DateTime e TimeSpan por meio do menu IntelliSense
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: eaa8a344e46c031b37b52106ba9aef25dac59b0c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290018"
---
# <a name="datetime-and-timespan-completion-through-intellisense-menu"></a>Conclusão de DateTime e TimeSpan por meio do menu IntelliSense

Esta refatoração aplica-se a:

- C#

**O que:** A conclusão de literal de cadeia de caracteres DateTime e TimeSpan por meio do menu IntelliSense.

**Quando:** Você deseja gravar os literais de cadeia de caracteres DateTime e TimeSpan. O IntelliSense fornece uma conclusão básica e uma explicação sobre o que significa cada um dos caracteres. 

**Por que:** Lembrar de formatos DateTime é difícil e o IntelliSense pode ajudá-lo a escrevê-lo.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor no literal da cadeia de caracteres DateTime ou TimeSpan.
2. Pressione **Ctrl** + **espaço** para disparar o menu **IntelliSense** .
3. Selecione o caractere que você deseja adicionar.

   ![Conclusão de DateTime do IntelliSense](media/datetime-completion.png)

## <a name="see-also"></a>Veja também

- [Refatoração](../refactoring-in-visual-studio.md)
