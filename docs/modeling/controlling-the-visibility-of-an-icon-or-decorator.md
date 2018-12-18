---
title: Controlando a visibilidade de um ícone ou decorador
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: a46509fb55c3d99c3cb2920dd6088497f326ab08
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49895483"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>Controlando a visibilidade de um ícone ou decorador
Um *decorador* é um ícone ou uma linha de texto que aparece em uma forma em uma linguagem específica de domínio (DSL). Você pode fazer o decorador aparecem e desaparecem dependendo do estado das propriedades no modelo. Por exemplo, em uma forma que representa uma pessoa, você poderia ter diferentes ícones que aparecem, dependendo do sexo da pessoa, número de filhos e assim por diante.

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>Controlando a visibilidade de um ícone ou decorador
 O procedimento a seguir pressupõe que você já definiu uma forma e seu mapeamento para uma classe de domínio. Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md).

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>Para controlar a visibilidade de um decorador de texto ou ícone

1. No diagrama de definição de DSL, adicione à classe forma os ícones ou decoradores de texto que você deseja exibir.

   1.  A classe shape do botão direito do mouse, aponte para **adicionar**e, em seguida, clique no tipo necessário de decorador.

   2.  Defina o decorador **posição** propriedade. Mais de um decorador pode ter a mesma posição. Por exemplo, você poderia ter ícones para masculino e feminino, compartilhando a mesma posição.

   3.  Defina as **ícone padrão** propriedade de um decorador de ícone.

2. Selecione o mapa de elemento de diagrama, que é a linha cinza entre a classe de forma e a classe de domínio no diagrama de definição de DSL.

3. Na janela de detalhes de DSL, na **mapas do decorador** guia, selecione um decorador. Por exemplo, o MaleDecorator.

4. Verifique as **filtro de visibilidade** caixa.

5. Se a propriedade de domínio que deve controlar a visibilidade está na classe de domínio imediata, deixe **caminho para a propriedade de filtro** em branco.

    Caso contrário, clique no menu suspenso e navegue até a relação ou onde se encontra a propriedade de classe.

   -   Para evitar um relatório de erros, você não deve navegar por meio de uma relação marcada com "*" na ferramenta de navegação.

6. Defina as **propriedade Filter** para uma propriedade de domínio. Por exemplo, sexo.

7. No **entradas de visibilidade** lista, adicione os valores dessa propriedade de domínio para o qual o decorador deve estar visível. Por exemplo, masculino.

8. Repita as etapas para cada ícone.

9. **Transformar todos os modelos**, compilar e executar e abrir um diagrama de teste.

10. Quando você altera o valor da propriedade de controle, os decoradores devem aparecer e desaparecer.

    Com frequência, convém visibilidade controlado por uma fórmula mais complexa que um conjunto simple de valores. Por exemplo, para ter um ícone dependem do número de links de um tipo específico ou para torná-lo dependem uma se um número é em um intervalo específico. Nesse caso, use o procedimento a seguir.

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>Para controlar a visibilidade de um decorador com base em uma fórmula

1.  Adicione uma propriedade de domínio calculado para a classe de domínio. No **propriedades** janela, defina os seguintes valores:

     **IsBrowsable =**`False`**-Isso oculta a propriedade do usuário**

     **Tipo =**`Calculated`**-isso significa que você irá fornecer código que calcula seu valor**

     **Nome da** por exemplo **DecoratorControl**

     **Tipo** = `Boolean`

     Para obter mais informações, consulte [Calculated e propriedades de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md).

2.  Verifique a nova propriedade para controlar a visibilidade de decorador.

    1.  Selecione o mapa de elemento de diagrama, que é a linha cinza da classe de domínio para a forma. No **detalhes de DSL** janela, abra o **DecoratorMap** guia.

    2.  Verifique as **filtro de visibilidade** caixa.

    3.  Na **propriedade Filter**, selecione a propriedade de controle **DecoratorControl**.

    4.  Sob **entradas de visibilidade**, insira `True`.

3.  Clique em **transformar todos os modelos** na **Gerenciador de soluções** barra de ferramentas.

4.  Clique em **compilar solução** sobre o **Build** menu.

5.  Clique duas vezes o relatório de erro foi exibido: "*YourClass* não contém uma definição para GetDecoratorControlValue...".

     Abre o editor de texto em dsl\generatedcode\domainclasses.cs. Acima do erro realçado é um comentário que solicita que você adicione um método.

6.  Observe o namespace de classe e método que estão faltando.  Por exemplo, Company.FamilyTree.Person.GetDecoratorControlValue().

7.  Em um arquivo de código separado, escreva uma definição de classe parcial que contém o método ausente. Por exemplo:

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     Para obter mais informações sobre como personalizar o modelo com o código do programa, consulte [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

8.  Recompile e execute a solução.

## <a name="see-also"></a>Consulte também

- [Definindo formas e conectores](../modeling/defining-shapes-and-connectors.md)
- [Configurando uma imagem de tela de fundo em um diagrama](../modeling/setting-a-background-image-on-a-diagram.md)
- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)