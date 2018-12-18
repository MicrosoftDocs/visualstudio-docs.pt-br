---
title: Gerar substituições de método Equals e GetHashCode em C#
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 5ec552e320b0c19c5c05e145fd9c5a4588f31b4c
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295703"
---
# <a name="generate-equals-and-gethashcode-method-overrides-in-visual-studio"></a>Gerar substituições dos métodos Equals e GetHashCode no Visual Studio

Esta geração de código aplica-se a:

- C#

**O quê:** Permite que você gere os métodos **Equals** e **GetHashCode**.

**Quando:** gere essas substituições quando houver um tipo que precise ser comparado por um ou mais campos e não pelo local do objeto na memória.

**Por que:**

- Se você estiver implementando um tipo de valor, considere substituir o método **Equals** para aumentar desempenho em relação à implementação padrão do método Equals em ValueType.

- Se você estiver implementando um tipo de referência, considere substituir o método **Equals** se o seu tipo parecer um tipo base, como Point, String, BigNumber e assim por diante.

- Substitua o método **GetHashCode** para permitir que um tipo funcione corretamente em uma tabela de hash. Leia mais orientação em [operadores de igualdade](/dotnet/standard/design-guidelines/equality-operators).

## <a name="how-to"></a>Como fazer

1. Coloque o cursor em algum lugar na linha de sua declaração de tipo.

   ![Código realçado](media/overrides-highlight-cs.png)

   > [!TIP]
   > Se você clicar duas vezes para selecionar o nome do tipo, a opção de menu não ficará disponível. Basta colocar o cursor em algum lugar na linha.

1. Depois, siga um destes procedimentos:

   - Pressione **Ctrl**+**.** para acionar o menu **Ações e Refatorações Rápidas**.

   - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.

   - Clique no ícone de ![chave de fenda](../media/screwdriver-icon.png) ícone que aparece na margem esquerda.

   ![Visualização Gerar substituições](media/overrides-preview-cs.png)

1. Selecione **Gerar Equals(object)** ou **Gerar Equals e GetHashCode** no menu suspenso.

1. Na caixa de diálogo **Selecionar membros**, escolha os membros para os quais deseja gerar os métodos:

    ![Caixa de diálogo Gerar substituições](media/overrides-dialog-cs.png)

    > [!TIP]
    > Você também pode optar por gerar operadores nessa caixa de diálogo usando a caixa de seleção na parte inferior da caixa de diálogo.

   Os métodos `Equals` e `GetHashCode` são gerados com implementações padrão.

   ![Resultado da geração do método](media/overrides-result-cs.png)

## <a name="see-also"></a>Consulte também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar alterações](../../ide/preview-changes.md)