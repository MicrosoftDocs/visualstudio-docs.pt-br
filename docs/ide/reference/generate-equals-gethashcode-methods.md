---
title: Gerar substituições de método Equals e GetHashCode em C#
description: Saiba como usar o menu ações rápidas e refatoração para gerar métodos Equals e GetHashCode.
ms.custom: SEO-VS-2020
ms.date: 03/08/2021
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 6a9d0ea6f6cb0aedc4fa13a8014b1a8bd66ccca0
ms.sourcegitcommit: 6ed6ae5a1693607dce57923a78d01eea3d88b29a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102514928"
---
# <a name="generate-equals-and-gethashcode-method-overrides-in-visual-studio"></a>Gerar substituições dos métodos Equals e GetHashCode no Visual Studio

Esta geração de código aplica-se a:

- C#

**O quê:** Permite que você gere os métodos **Equals** e **GetHashCode**.

**Quando:** gere essas substituições quando houver um tipo que precise ser comparado por um ou mais campos e não pelo local do objeto na memória.

**Por**

- Se você estiver implementando um tipo de valor, considere substituir o método **Equals** . Você pode obter um desempenho maior sobre a implementação padrão do método Equals no ValueType ao fazer isso.

- Se você estiver implementando um tipo de referência, considere substituir o método **Equals** se o seu tipo for semelhante a um tipo base, como Point, String, BigNumber e assim por diante.

- Substitua o método **GetHashCode** para permitir que um tipo funcione corretamente em uma tabela de hash. Leia mais orientação em [operadores de igualdade](/dotnet/standard/design-guidelines/equality-operators).

## <a name="how-to"></a>Como fazer

1. Coloque o cursor em algum lugar na linha de sua declaração de tipo.

    ```csharp
    public class ImaginaryNumber
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }
    }
    ```

   Seu código deve ser semelhante à captura de tela a seguir:

   ![Captura de tela do código realçado no qual aplicar o método gerado](media/overrides-highlight-cs.png)

   > [!TIP]
   > Se você clicar duas vezes para selecionar o nome do tipo, a opção de menu não ficará disponível. Basta colocar o cursor em algum lugar na linha.

1. Em seguida, escolha uma das seguintes ações:

   - Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.

   - Clique com o botão direito do mouse e selecione o menu **Ações Rápidas e Refatorações**.

   - Clique no botão ![Captura de tela do ícone de chave de fenda de ações rápidas no Visual Studio](../media/screwdriver-icon.png) ícone que aparece na margem esquerda.

1. Selecione **Gerar Equals(object)** ou **Gerar Equals e GetHashCode** no menu suspenso.

   ![Captura de tela do menu suspenso gerar substituições](media/overrides-preview-cs.png)

1. Na caixa de diálogo **Selecionar membros**, escolha os membros para os quais deseja gerar os métodos:

    ![Caixa de diálogo Gerar substituições](media/overrides-dialog-cs.png)

    > [!TIP]
    > Você também pode optar por gerar operadores nessa caixa de diálogo usando a caixa de seleção na parte inferior da caixa de diálogo.

   Os `Equals` `GetHashCode` métodos e são gerados com implementações padrão, conforme mostrado no código a seguir:

    ```csharp
   public class ImaginaryNumber : IEquatable<ImaginaryNumber>
    {
        public double RealNumber { get; set; }
        public double ImaginaryUnit { get; set; }

        public override bool Equals(object obj)
        {
            return Equals(obj as ImaginaryNumber);
        }

        public bool Equals(ImaginaryNumber other)
        {
            return other != null &&
                   RealNumber == other.RealNumber &&
                   ImaginaryUnit == other.ImaginaryUnit;
        }

        public override int GetHashCode()
        {
            return HashCode.Combine(RealNumber, ImaginaryUnit);
        }
    }
    ```

   Seu código deve ser semelhante à captura de tela a seguir:

   ![Captura de tela do resultado do método gerado](media/overrides-result-cs.png)

## <a name="see-also"></a>Consulte também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)
