---
title: Gerar operadores de comparação para tipos que implementam IComparable
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 31e33b562a5a11ff77c1d610fbce9e90506b036d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290017"
---
# <a name="generate-comparison-operators-for-types-that-implement-icomparable"></a>Gerar operadores de comparação para tipos que implementam IComparable

Esta geração de código aplica-se a:

- C#

**O que:** Permite gerar operadores de **comparação** para tipos que implementam IComparable.

**Quando:** Você tem um tipo que implementa IComparable, adicionaremos automaticamente os operadores de comparação.

**Por que:** Se você estiver implementando um tipo de valor, considere substituir o método **Equals** para obter um desempenho maior sobre a implementação padrão do método Equals em ValueType.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor dentro da classe ou na palavra-chave IComparable.

2. Depois, siga um destes procedimentos:

   - Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

   - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.

   - Clique no botão ![chave de fenda](../media/screwdriver-icon.png) ícone que aparece na margem esquerda.

   ![Gerar Operadores de Comparação](media/generate-comparison-operators.png)

3. Selecione **gerar Equals (Object)** no menu suspenso.

## <a name="see-also"></a>Veja também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)
