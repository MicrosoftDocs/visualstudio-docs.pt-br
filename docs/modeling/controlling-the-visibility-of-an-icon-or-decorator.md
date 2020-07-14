---
title: Controlando a visibilidade de um ícone ou decorador
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d2082f7e26d3e335ed88bbced0f59d6d6c4780c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546634"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>Controlando a visibilidade de um ícone ou decorador
Um *decorador* é um ícone ou linha de texto que aparece em uma forma em uma DSL (linguagem específica do domínio). Você pode fazer com que o decorador apareça e desapareça, dependendo do estado das propriedades no modelo. Por exemplo, em uma forma que representa uma pessoa, você poderia ter ícones diferentes que aparecem dependendo do sexo da pessoa, do número de filhos e assim por diante.

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>Controlando a visibilidade de um ícone ou decorador
 O procedimento a seguir pressupõe que você já definiu uma forma e seu mapeamento para uma classe de domínio. Para obter mais informações, consulte [como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md).

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>Para controlar a visibilidade de um ícone ou decorador de texto

1. No diagrama de definição de DSL, adicione à classe forma os ícones ou decoradores de texto que você deseja exibir.

   1. Clique com o botão direito do mouse na classe Shape, aponte para **Adicionar**e clique no tipo de decorador necessário.

   2. Defina a propriedade **Position** do decorador. Mais de um decorador pode ter a mesma posição. Por exemplo, você pode ter ícones para macho e fêmea compartilhando a mesma posição.

   3. Defina a propriedade **ícone padrão** de um decorador de ícone.

2. Selecione o mapa do elemento de diagrama, que é a linha cinza entre a classe Shape e a classe de domínio no diagrama de definição de DSL.

3. Na janela detalhes de DSL, na guia **mapas de decoradores** , selecione um decorador. Por exemplo, o MaleDecorator.

4. Marque a caixa **filtro de visibilidade** .

5. Se a propriedade de domínio que deve controlar a visibilidade estiver na classe de domínio Immediate, deixe **caminho para a propriedade de filtro** em branco.

    Caso contrário, clique no menu suspenso e navegue até a relação ou a classe na qual a propriedade está localizada.

   - Para evitar um relatório de erros, você não deve navegar por uma relação marcada com "*" na ferramenta de navegação.

6. Defina a **propriedade de filtro** como uma propriedade de domínio. Por exemplo, sexo.

7. Na lista **entradas de visibilidade** , adicione valores dessa propriedade de domínio para os quais o decorador deve estar visível. Por exemplo, masculino.

8. Repita as etapas para cada ícone.

9. **Transforme todos os modelos**, compile e execute e abra um diagrama de teste.

10. Quando você altera o valor da propriedade de controle, os decoradores devem aparecer e desaparecer.

    Frequentemente, você deseja que a visibilidade seja controlada por uma fórmula mais complexa do que um conjunto simples de valores. Por exemplo, para que um ícone dependa do número de links de um determinado tipo, ou para que ele dependa de um número em um determinado intervalo. Nesse caso, use o procedimento a seguir.

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>Para controlar a visibilidade de um decorador com base em uma fórmula

1. Adicione uma propriedade de domínio calculada à classe de domínio. Na janela **Propriedades** , defina os seguintes valores:

     **Isnavegável =** `False` **-isso oculta a propriedade do usuário**    

     **Tipo =** `Calculated` **-isso significa que você fornecerá um código que calcula seu valor**    

     **Nome** , por exemplo **DecoratorControl**

     **Escreva** = `Boolean`

     Para obter mais informações, consulte [Propriedades de armazenamento calculadas e personalizadas](../modeling/calculated-and-custom-storage-properties.md).

2. Faça com que a nova propriedade controle a visibilidade do decorador.

    1. Selecione o mapa do elemento de diagrama, que é a linha cinza da classe de domínio para a forma. Na janela **detalhes de DSL** , abra a guia **DecoratorMap** .

    2. Marque a caixa **filtro de visibilidade** .

    3. Na **propriedade de filtro**, selecione a propriedade de controle **DecoratorControl**.

    4. Em **entradas de visibilidade**, insira `True` .

3. Clique em **transformar todos os modelos** na barra de ferramentas **Gerenciador de soluções** .

4. Clique em **Compilar solução** no menu **Compilar** .

5. Clique duas vezes no relatório de erros que apareceu: "*yourClass* não contém uma definição para GetDecoratorControlValue...".

     O editor de texto é aberto em Dsl\GeneratedCode\DomainClasses.cs. Acima do erro realçado há um comentário que solicita que você adicione um método.

6. Observe o namespace, a classe e o método que estão ausentes.  Por exemplo, empresa. FamilyTree. Person. GetDecoratorControlValue ().

7. Em um arquivo de código separado, escreva uma definição de classe parcial que contenha o método ausente. Por exemplo:

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     Para obter mais informações sobre como personalizar o modelo com o código do programa, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

8. Recompile e execute a solução.

## <a name="see-also"></a>Confira também

- [Definindo formas e conectores](../modeling/defining-shapes-and-connectors.md)
- [Definindo uma imagem de plano de fundo em um diagrama](../modeling/setting-a-background-image-on-a-diagram.md)
- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)