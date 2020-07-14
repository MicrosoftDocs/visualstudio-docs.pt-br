---
title: Personalizando a criação e o movimento de elementos
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.elementmergedirective
helpviewer_keywords:
- Domain-Specific Language, element merge directives
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a94f1e3321d846578ea42c69e50d48713ff618fb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547258"
---
# <a name="customizing-element-creation-and-movement"></a>Personalizando a criação e o movimento de elementos

Você pode permitir que um elemento seja arrastado para outro, seja na caixa de ferramentas ou em uma operação de colar ou mover. Você pode ter os elementos movidos vinculados aos elementos de destino, usando as relações que você especificar.

Uma diretiva de mesclagem de elementos (EMD) especifica o que acontece quando um elemento de modelo é *mesclado* em outro elemento de modelo. Isso ocorre quando:

- O usuário arrasta da caixa de ferramentas para o diagrama ou para uma forma.

- O usuário cria um elemento usando um menu Adicionar no Explorer ou uma forma de compartimento.

- O usuário move um item de uma raia para outra.

- O usuário cola um elemento.

- O código do programa chama a diretiva de mesclagem de elementos.

Embora as operações de criação possam parecer diferentes das operações de cópia, elas realmente funcionam da mesma maneira. Quando um elemento é adicionado, por exemplo, da caixa de ferramentas, um protótipo dele é replicado. O protótipo é mesclado no modelo da mesma maneira que os elementos que foram copiados de outra parte do modelo.

A responsabilidade de um EMD é decidir como um objeto ou grupo de objetos deve ser mesclado em um local específico no modelo. Em particular, ele decide quais relações devem ser instanciadas para vincular o grupo mesclado ao modelo. Você também pode personalizá-lo para definir propriedades e criar objetos adicionais.

![EMD DSL&#45;&#95;mesclar](../modeling/media/dsl-emd_merge.png)

Um EMD é gerado automaticamente quando você define uma relação de incorporação. Esse EMD padrão cria uma instância da relação quando os usuários adicionam novas instâncias filho ao pai. Você pode modificar esses EMDs padrão, por exemplo, adicionando código personalizado.

Você também pode adicionar seu próprio EMDs na definição de DSL, para permitir que os usuários arrastem ou colem combinações diferentes de classes mescladas e de recebimento.

## <a name="defining-an-element-merge-directive"></a>Definindo uma diretiva de mesclagem de elementos

Você pode adicionar diretivas de mesclagem de elementos a classes de domínio, relações de domínio, formas, conectores e diagramas. Você pode adicioná-los ou localizá-los no Gerenciador de DSL na classe de domínio de recebimento. A classe de recebimento é a classe de domínio do elemento que já está no modelo e para o qual o elemento novo ou copiado será mesclado.

![Detalhes de&#45;de DSL&#95;EMD](../modeling/media/dsl-emd_details.png)

A **classe de indexação** é a classe de domínio dos elementos que podem ser mesclados em membros da classe de recebimento. As instâncias de subclasses da classe de indexação também serão mescladas por esse EMD, a menos que você defina **aplica-se a subclasses** como false.

Há dois tipos de diretiva de mesclagem:

- Uma diretiva de **mesclagem de processo** especifica as relações pelas quais o novo elemento deve ser vinculado à árvore.

- Uma diretiva de **mesclagem de encaminhamento** redireciona o novo elemento para outro elemento receptor, normalmente um pai.

Você pode adicionar código personalizado para mesclar diretivas:

- Set **usa a aceitação personalizada** para adicionar seu próprio código para determinar se uma determinada instância do elemento de indexação deve ser mesclada no elemento de destino. Quando o usuário arrasta da caixa de ferramentas, o ponteiro "Invalid" mostra se o seu código não permite a mesclagem.

   Por exemplo, você pode permitir a mesclagem somente quando o elemento receptor estiver em um estado específico.

- Set **usa mesclagem personalizada** para adicionar fornecer código próprio para definir as alterações feitas no modelo quando a mesclagem é executada.

   Por exemplo, você pode definir propriedades no elemento mesclado usando dados de seu novo local no modelo.

> [!NOTE]
> Se você escrever um código de mesclagem personalizado, ele afetará somente as mesclagens executadas usando esse EMD. Se houver outros EMDs que mesclam o mesmo tipo de objeto, ou se houver outro código personalizado que crie esses objetos sem usar o EMD, eles não serão afetados pelo seu código de mesclagem personalizado.
>
> Se você quiser garantir que um novo elemento ou uma nova relação seja sempre processada pelo seu código personalizado, considere definir um `AddRule` na relação de incorporação e um `DeleteRule` na classe de domínio do elemento. Para obter mais informações, consulte [regras propagar alterações no modelo](../modeling/rules-propagate-changes-within-the-model.md).

## <a name="example-defining-an-emd-without-custom-code"></a>Exemplo: definindo um EMD sem código personalizado

O exemplo a seguir permite que os usuários criem um elemento e um conector ao mesmo tempo arrastando da caixa de ferramentas para uma forma existente. O exemplo adiciona um EMD à definição de DSL. Antes dessa modificação, os usuários podem arrastar ferramentas para o diagrama, mas não para as formas existentes.

Os usuários também podem colar elementos em outros elementos.

### <a name="to-let-users-create-an-element-and-a-connector-at-the-same-time"></a>Para permitir que os usuários criem um elemento e um conector ao mesmo tempo

1. Crie uma nova DSL usando o modelo de solução de **linguagem mínima** .

    Quando você executa essa DSL, ela permite criar formas e conectores entre as formas. Você não pode arrastar uma nova forma de **exemploelement** da caixa de ferramentas para uma forma existente.

2. Para permitir que os usuários mesclem elementos em `ExampleElement` formas, crie um novo EMD na `ExampleElement` classe de domínio:

   1. No **Gerenciador de DSL**, expanda **classes de domínio**. Clique com o botão direito do mouse `ExampleElement` e clique em **Adicionar nova diretiva de mesclagem de elemento**.

   2. Verifique se a janela **detalhes de DSL** está aberta, para que você possa ver os detalhes do novo EMD. (Menu: **Exibir**, **outras janelas**, **detalhes de DSL**.)

3. Defina a **classe de indexação** na janela detalhes de DSL para definir qual classe de elementos pode ser mesclada em `ExampleElement` objetos.

    Para este exemplo, selecione `ExampleElements` , para que o usuário possa arrastar novos elementos para os elementos existentes.

    Observe que a classe de indexação se torna o nome do EMD no Gerenciador de DSL.

4. Em **mesclar processo, criando links**, adicione dois caminhos:

   - Um caminho vincula o novo elemento ao modelo pai. A expressão de caminho que você precisa inserir navega do elemento existente, até a relação de incorporação ao modelo pai. Por fim, ele especifica a função no novo link ao qual o novo elemento será atribuído. O caminho é o seguinte:

      `ExampleModelHasElements.ExampleModel/!ExampleModel/.Elements`

   - O outro caminho vincula o novo elemento ao elemento existente. A expressão de caminho Especifica a relação de referência e a função à qual o novo elemento será atribuído. Esse caminho é o seguinte:

      `ExampleElementReferencesTargets.Sources`

      Você pode usar a ferramenta de navegação de caminho para criar cada caminho:

      1. Em **mesclar processo, criando links em caminhos**, clique em **\<add path>** .

      2. Clique na seta suspensa à direita do item de lista. Uma exibição de árvore é exibida.

      3. Expanda os nós na árvore para formar o caminho que você deseja especificar.

5. Testar a DSL:

   1. Pressione **F5** para recompilar e executar a solução.

        A recompilação levará mais tempo do que o normal, pois o código gerado será atualizado de modelos de texto para estar em conformidade com a nova definição de DSL.

   2. Quando a instância experimental do Visual Studio for iniciada, abra um arquivo de modelo de sua DSL. Crie alguns elementos de exemplo.

   3. Arraste da ferramenta de **elemento de exemplo** para uma forma existente.

        Uma nova forma é exibida e está vinculada à forma existente com um conector.

   4. Copiar uma forma existente. Selecione outra forma e Cole.

        Uma cópia da primeira forma é criada.  Ele tem um novo nome e está vinculado à segunda forma com um conector.

Observe os seguintes pontos deste procedimento:

- Criando diretivas de mesclagem de elementos, você pode permitir que qualquer classe de elemento aceite qualquer outra. O EMD é criado na classe de domínio de recebimento e a classe de domínio aceito é especificada no campo **classe de índice** .

- Ao definir caminhos, você pode especificar quais links devem ser usados para conectar o novo elemento ao modelo existente.

     Os links que você especificar devem incluir uma relação incorporada.

- O EMD afeta a criação da caixa de ferramentas e também as operações de colagem.

     Se você escrever um código personalizado que cria novos elementos, poderá invocar explicitamente o EMD usando o `ElementOperations.Merge` método. Isso garante que o código vincule novos elementos ao modelo da mesma maneira que outras operações. Para obter mais informações, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).

## <a name="example-adding-custom-accept-code-to-an-emd"></a>Exemplo: adicionando código de aceitação personalizado a um EMD

Ao adicionar o código personalizado a um EMD, você pode definir um comportamento de mesclagem mais complexo. Este exemplo simples impede que o usuário adicione mais do que um número fixo de elementos ao diagrama. O exemplo modifica o EMD padrão que acompanha uma relação de incorporação.

### <a name="to-write-custom-accept-code-to-restrict-what-the-user-can-add"></a>Para gravar o código de aceitação personalizado para restringir o que o usuário pode adicionar

1. Crie uma DSL usando o modelo de solução de **linguagem mínima** . Abra o diagrama de definição de DSL.

2. No Gerenciador de DSL, expanda **classes de domínio**, `ExampleModel` e **diretivas de mesclagem de elemento**. Selecione a diretiva de mesclagem de elementos que é nomeada `ExampleElement` .

     Esse EMD controla como o usuário pode criar novos `ExampleElement` objetos no modelo, por exemplo, arrastando da caixa de ferramentas.

3. Na janela **detalhes de DSL** , selecione **usa aceitação personalizada**.

4. Recriar a solução. Isso levará mais tempo do que o normal, pois o código gerado será atualizado a partir do modelo.

     Um erro de compilação será relatado, semelhante a: "Company. ElementMergeSample. Exampleelement não contém uma definição para CanMergeExampleElement..."

     Você deve implementar o método `CanMergeExampleElement` .

5. Crie um novo arquivo de código no projeto **DSL** . Substitua seu conteúdo pelo código a seguir e altere o namespace para o namespace do seu projeto.

    ```csharp
    using Microsoft.VisualStudio.Modeling;

    namespace Company.ElementMergeSample // EDIT.
    {
      partial class ExampleModel
      {
        /// <summary>
        /// Called whenever an ExampleElement is to be merged into this ExampleModel.
        /// This happens when the user pastes an ExampleElement
        /// or drags from the toolbox.
        /// Determines whether the merge is allowed.
        /// </summary>
        /// <param name="rootElement">The root element in the merging EGP.</param>
        /// <param name="elementGroupPrototype">The EGP that the user wants to merge.</param>
        /// <returns>True if the merge is allowed</returns>
        private bool CanMergeExampleElement(ProtoElementBase rootElement, ElementGroupPrototype elementGroupPrototype)
        {
          // Allow no more than 4 elements to be added:
          return this.Elements.Count < 4;
        }
      }
    }
    ```

    Este exemplo simples restringe o número de elementos que podem ser mesclados no modelo pai. Para condições mais interessantes, o método pode inspecionar qualquer uma das propriedades e links do objeto de recebimento. Ele também pode inspecionar as propriedades dos elementos de mesclagem, que são transportados em um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> . Para obter mais informações sobre o `ElementGroupPrototypes` , consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md). Para obter mais informações sobre como escrever código que lê um modelo, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

6. Testar a DSL:

    1. Pressione **F5** para recompilar a solução. Quando a instância experimental do Visual Studio for aberta, abra uma instância de sua DSL.

    2. Crie novos elementos de várias maneiras:

        - Arraste da ferramenta de **elemento de exemplo** para o diagrama.

        - No **Gerenciador de modelos de exemplo**, clique com o botão direito do mouse no nó raiz e clique em **Adicionar novo elemento de exemplo**.

        - Copie e cole um elemento no diagrama.

    3. Verifique se você não pode usar nenhuma dessas maneiras para adicionar mais de quatro elementos ao modelo. Isso ocorre porque todos usam a diretiva de mesclagem de elementos.

## <a name="example-adding-custom-merge-code-to-an-emd"></a>Exemplo: adicionando um código de mesclagem personalizado a um EMD

No código de mesclagem personalizado, você pode definir o que acontece quando o usuário arrasta uma ferramenta ou cola em um elemento. Há duas maneiras de definir uma mesclagem personalizada:

1. Set **usa mesclagem personalizada** e fornece o código necessário. Seu código substitui o código de mesclagem gerado. Use esta opção se desejar redefinir completamente o que a mesclagem faz.

2. Substitua o `MergeRelate` método e, opcionalmente, o `MergeDisconnect` método. Para fazer isso, você deve definir a propriedade **derivada dupla** da classe de domínio. Seu código pode chamar o código de mesclagem gerado na classe base. Use esta opção se você quiser executar operações adicionais depois que a mesclagem tiver sido executada.

   Essas abordagens afetam apenas as mesclagens que são executadas usando esse EMD. Se você quiser afetar todas as maneiras em que o elemento mesclado pode ser criado, uma alternativa é definir um `AddRule` na relação de incorporação e um `DeleteRule` na classe de domínio mesclado. Para obter mais informações, consulte [regras propagar alterações no modelo](../modeling/rules-propagate-changes-within-the-model.md).

### <a name="to-override-mergerelate"></a>Para substituir MergeRelate

1. Na definição de DSL, certifique-se de que você definiu o EMD para o qual você deseja adicionar o código. Se desejar, você pode adicionar caminhos e definir o código de aceitação personalizado conforme descrito nas seções anteriores.

2. No diagrama DslDefinition, selecione a classe de recebimento da mesclagem. Normalmente, é a classe na extremidade de origem de uma relação incorporada.

     Por exemplo, em uma DSL gerada a partir da solução de linguagem mínima, selecione `ExampleModel` .

3. Na janela **Propriedades** , Set **gera Double derivado** como **true**.

4. Recriar a solução.

5. Inspecione o conteúdo de **Dsl\Generated Files\DomainClasses.cs**. Procure métodos chamados `MergeRelate` e examine seu conteúdo. Isso ajudará você a escrever suas próprias versões.

6. Em um novo arquivo de código, escreva uma classe parcial para a classe de recebimento e substitua o `MergeRelate` método. Lembre-se de chamar o método base. Por exemplo:

    ```csharp
    partial class ExampleModel
    {
      /// <summary>
      /// Called when the user drags or pastes an ExampleElement onto the diagram.
      /// Sets the time of day as the name.
      /// </summary>
      /// <param name="sourceElement">Element to be added</param>
      /// <param name="elementGroup">Elements to be merged</param>
      protected override void MergeRelate(ModelElement sourceElement, ElementGroup elementGroup)
      {
        // Connect the element according to the EMD:
        base.MergeRelate(sourceElement, elementGroup);

        // Custom actions:
        ExampleElement mergingElement = sourceElement as ExampleElement;
        if (mergingElement != null)
        {
          mergingElement.Name = DateTime.Now.ToLongTimeString();
        }
      }
    }
    ```

### <a name="to-write-custom-merge-code"></a>Para gravar o código de mesclagem personalizado

1. Em **Dsl\Generated Code\DomainClasses.cs**, inspecione os métodos chamados `MergeRelate` . Esses métodos criam links entre um novo elemento e o modelo existente.

    Além disso, inspecione os métodos chamados `MergeDisconnect` . Esses métodos desvinculam um elemento do modelo quando ele deve ser excluído.

2. No **Gerenciador de DSL**, selecione ou crie a diretiva de mesclagem de elementos que você deseja personalizar. Na janela **detalhes de DSL** , definir **usa mesclagem personalizada**.

    Quando você define essa opção, as opções de mesclagem de **processo de mesclagem** e **encaminhamento** são ignoradas. Seu código é usado em vez disso.

3. Recriar a solução. Levará mais tempo do que o normal, pois os arquivos de código gerados serão atualizados a partir do modelo.

    As mensagens de erro serão exibidas. Clique duas vezes nas mensagens de erro para ver as instruções no código gerado. Essas instruções solicitam que você forneça dois métodos, `MergeRelate` *YourDomainClass* e `MergeDisconnect` *YourDomainClass*

4. Escreva os métodos em uma definição de classe parcial em um arquivo de código separado. Os exemplos inspecionados anteriormente devem sugerir o que você precisa.

   O código de mesclagem personalizado não afetará o código que cria objetos e relações diretamente e não afetará outros EMDs. Para garantir que suas alterações adicionais sejam implementadas independentemente de como o elemento é criado, considere escrever um `AddRule` e um `DeleteRule` em vez disso. Para obter mais informações, consulte [regras propagar alterações no modelo](../modeling/rules-propagate-changes-within-the-model.md).

## <a name="redirecting-a-merge-operation"></a>Redirecionando uma operação de mesclagem

Uma diretiva de mesclagem direta redireciona o destino de uma operação de mesclagem. Normalmente, o novo destino é o pai de inserção do destino inicial.

Por exemplo, em uma DSL que foi criada com o modelo de diagrama de componente, as portas são inseridas em componentes. As portas são exibidas como pequenas formas na borda de uma forma de componente. O usuário cria portas arrastando a ferramenta de porta para uma forma de componente. Mas, às vezes, o usuário arrasta erroneamente a ferramenta de porta para uma porta existente, em vez do componente, e a operação falha. Isso é um erro fácil quando há várias portas existentes. Para ajudar o usuário a evitar esse incômodo, você pode permitir que as portas sejam arrastadas para uma porta existente, mas que tenham a ação redirecionada para o componente pai. A operação funciona como se o elemento de destino fosse o componente.

Você pode criar uma diretiva de mesclagem direta na solução de modelo de componente. Se você compilar e executar a solução original, verá que os usuários podem arrastar qualquer número de elementos de porta de **entrada** ou de **porta de saída** da **caixa de ferramentas** para um elemento de **componente** . No entanto, eles não podem arrastar uma porta para uma porta existente. O ponteiro indisponível alerta-os de que essa movimentação não está habilitada. No entanto, você pode criar uma diretiva de mesclagem direta para que uma porta que seja descartada de forma não intencional em uma **porta de entrada** existente seja encaminhada para o elemento de **componente** .

### <a name="to-create-a-forward-merge-directive"></a>Para criar uma diretiva de mesclagem direta

1. Crie uma [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] solução usando o modelo de modelo de componente.

2. Exiba o **Gerenciador de DSL** , abrindo DslDefinition. DSL.

3. No **Gerenciador de DSL**, expanda **classes de domínio**.

4. A classe de domínio **ComponentPort** abstract é a classe base de **inport** e **Outport**. Clique com o botão direito do mouse em **ComponentPort** e clique em **Adicionar nova diretiva de mesclagem de elementos**.

    Um novo nó de **diretiva de mesclagem de elementos** aparece sob o nó **diretivas de mesclagem de elementos** .

5. Selecione o nó **diretiva de mesclagem de elementos** e abra a janela detalhes de **DSL** .

6. Na lista classe de indexação, selecione **ComponentPort**.

7. Selecione **encaminhar mesclagem para uma classe de domínio diferente**.

8. Na lista seleção de caminho, expanda **ComponentPort**, expanda **ComponentHasPorts**e selecione **componente**.

    O novo caminho deve ser semelhante a este:

    **Componente ComponentHasPorts. Component/!**

9. Salve a solução e, em seguida, transforme os modelos clicando no botão mais à direita na barra de ferramentas **Gerenciador de soluções** .

10. Compile e execute a solução. Uma nova instância do Visual Studio é exibida.

11. Em **Gerenciador de soluções**, abra Sample. MyDSL. O diagrama e a **caixa de ferramentas ComponentLanguage** são exibidos.

12. Arraste uma **porta de entrada** da **caixa de ferramentas** para outra **porta de entrada.** Em seguida, arraste um **OutputPort** para um **InputPort** e, em seguida, para outro **OutputPort**.

     Você não verá o ponteiro indisponível e poderá descartar a nova **porta de entrada** no existente. Selecione a nova **porta de entrada** e arraste-a para outro ponto no **componente**.

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md)
- [Diagramas de circuito de exemplo DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
