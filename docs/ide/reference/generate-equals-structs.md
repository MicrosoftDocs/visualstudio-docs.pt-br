---
title: Gerar operadores IEquatable para structs
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ccc5be9debbdc2b4901d4aad15a0dc4d2bf1bb9f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290015"
---
# <a name="generate-iequatable-operators-when-generating-equals-for-structs"></a>Gerar operadores IEquatable ao gerar Equals para structs

Esta geração de código aplica-se a:

- C#

**O que:** Permite gerar operadores **Equals** e **IEquatable** para [structs](https://docs.microsoft.com/dotnet/csharp/language-reference/builtin-types/struct).

**Quando:** Você tem uma estrutura que adicionaremos automaticamente o IEquatable, bem como os operadores Equals e not Equals para você.

**Por**

- Se você estiver implementando um tipo de valor, considere substituir o método **Equals** para aumentar desempenho em relação à implementação padrão do método Equals em ValueType.

- Implementar a interface IEquatable implementa um método Equals () específico do tipo.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor em algum lugar na linha da sua declaração de struct.

2. Depois, siga um destes procedimentos:

   - Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

   - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.

   - Clique no botão ![chave de fenda](../media/screwdriver-icon.png) ícone que aparece na margem esquerda.

   ![Gerar IEquatable e Equals para structs](media/generate-equals-structs.png)

3. Selecione **gerar Equals (Object)** no menu suspenso.

## <a name="see-also"></a>Veja também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)
