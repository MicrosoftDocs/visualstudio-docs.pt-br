---
title: Personalizando a criação e o movimento de elementos
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.elementmergedirective
helpviewer_keywords:
- Domain-Specific Language, element merge directives
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 2181e9f89fc8d859bfda9a29de6af8726ae5aef3
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967422"
---
# <a name="customizing-element-creation-and-movement"></a>Personalizando a criação e o movimento de elementos

Você pode permitir que um elemento a ser arrastado para outro, na caixa de ferramentas ou em uma operação de colar ou a operação de movimentação. Você pode ter os elementos movidos vinculados aos elementos de destino, usando as relações que você especificar.

Uma diretiva element merge (EMD) Especifica o que acontece quando um elemento de modelo é *mesclada* em outro elemento de modelo. Isso acontece quando:

- O usuário arrasta Toolbox para o diagrama ou uma forma.

- O usuário cria um elemento usando um menu Adicionar no explorer ou uma forma de compartimento.

- O usuário move um item de uma raia para outra.

- O usuário cola um elemento.

- O código do programa chama a diretiva element merge.

Embora as operações de criação podem parecer diferente do que as operações de cópia, na verdade, eles funcionam da mesma maneira. Quando um elemento for adicionado, por exemplo da caixa de ferramentas, um protótipo dele será replicado. O protótipo é mesclado no modelo da mesma maneira como os elementos que foram copiados de outra parte do modelo.

A responsabilidade de uma EMD é decidir como um objeto ou grupo de objetos deve ser mesclado em um local específico no modelo. Em particular, ele decide quais relações devem ser instanciadas para vincular o grupo mesclado no modelo. Você também pode personalizá-lo para definir as propriedades e criar objetos adicionais.

![DSL&#45;EMD&#95;de mesclagem](../modeling/media/dsl-emd_merge.png)

Uma EMD é gerado automaticamente quando você define uma relação de incorporação. Esse padrão EMD cria uma instância da relação quando os usuários adicionarem novas instâncias filho ao pai. Você pode modificar essas EMDs padrão, por exemplo, adicionando código personalizado.

Você também pode adicionar seus próprios EMDs na definição de DSL, para permitir aos usuários arrastar ou colar combinações diferentes de classes mescladas e de recebimento.

## <a name="defining-an-element-merge-directive"></a>Definindo uma diretiva Element Merge

Você pode adicionar diretivas de mesclagem de elementos para as classes de domínio, relações de domínio, formas, conectores e diagramas. Você pode adicionar ou encontrá-los no Gerenciador de DSL sob a classe de domínio de recebimento. A classe de recebimento é a classe de domínio do elemento que já está no modelo e, para que o elemento novo ou copiado será mesclado.

![DSL&#45;EMD&#95;detalhes](../modeling/media/dsl-emd_details.png)

O **indexação classe** é a classe de domínio de elementos que podem ser mescladas em membros da classe receptora. Instâncias de subclasses da classe de indexação também serão mescladas por este EMD, a menos que você defina **aplica-se a subclasses** como False.

Há dois tipos de diretiva de mesclagem:

- Um **processo de mesclagem** diretiva especifica as relações pelo qual o novo elemento deve ser vinculado à árvore.

- Um **encaminhar mesclagem** diretiva redireciona o novo elemento para outro elemento de recebimento, normalmente um pai.

Você pode adicionar código personalizado para diretivas de mesclagem:

- Definir **aceitação personalizada usa** para adicionar seu próprio código para determinar se uma determinada instância do elemento a indexação deve ser mesclada no elemento de destino. Quando o usuário arrasta da caixa de ferramentas, o ponteiro "inválido" mostra se seu código não permite a mesclagem.

   Por exemplo, você pode permitir que a mesclagem apenas quando o elemento de recebimento está em um estado específico.

- Definir **mesclagem personalizada de usos** adicionar fornecem o próprio código para definir as alterações feitas no modelo quando a mesclagem é executada.

   Por exemplo, você pode definir propriedades no elemento mesclado usando dados de seu novo local no modelo.

> [!NOTE]
> Se você escrever código personalizado de mesclagem, ele afeta somente mesclagens que são executadas usando este EMD. Se não houver outros EMDs que a mesclagem do mesmo tipo de objeto, ou se não houver outro código personalizado que cria esses objetos sem usar o EMD, em seguida, eles não serão afetados pelo seu código personalizado de mesclagem.
>
> Se você quiser garantir que um novo elemento ou um novo relacionamento sempre é processado por seu código personalizado, considere definir uma `AddRule` sobre a relação de incorporação e um `DeleteRule` na classe de domínio do elemento. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).

## <a name="example-defining-an-emd-without-custom-code"></a>Exemplo: Definindo uma EMD sem código personalizado

O exemplo a seguir permite aos usuários criar um elemento e um conector ao mesmo tempo, arrastando da caixa de ferramentas para uma forma existente. O exemplo adiciona uma EMD a definição de DSL. Antes dessa modificação, os usuários podem arrastar as ferramentas para o diagrama, mas não para formas existentes.

Os usuários também podem colar elementos em outros elementos.

### <a name="to-let-users-create-an-element-and-a-connector-at-the-same-time"></a>Para permitir aos usuários criar um elemento e um conector ao mesmo tempo

1. Criar uma nova DSL usando o **linguagem mínima** modelo de solução.

    Quando você executa essa DSL, ele permite criar formas e conectores entre as formas. Não é possível arrastar um novo **ExampleElement** forma Toolbox para uma forma existente.

2. Para que os usuários a mesclagem de elementos no `ExampleElement` formas, crie um novo EMD no `ExampleElement` classe de domínio:

   1.  Na **Gerenciador de DSL**, expanda **Classes de domínio**. Clique com botão direito `ExampleElement` e, em seguida, clique em **adicionar nova diretiva Element Merge**.

   2.  Certifique-se de que o **detalhes de DSL** janela estiver aberta, para que você possa ver os detalhes de EMD o novo. (Menu: **modo de exibição**, **outros Windows**, **detalhes de DSL**.)

3. Defina as **classe de indexação** na janela de detalhes de DSL, para definir a classe de elementos pode ser mesclado com `ExampleElement` objetos.

    Neste exemplo, selecione `ExampleElements`, de modo que o usuário pode arrastar novos elementos para os elementos existentes.

    Observe que a classe de indexação se torna o nome da EMD no Gerenciador de DSL.

4. Sob **processa mesclagem Criando links**, adicionar dois caminhos:

   - Um caminho vincula o novo elemento para o modelo pai. A expressão de caminho que você precisa inserir navega de elemento existente, para cima através da relação de incorporação para o modelo pai. Por fim, ele especifica a função no novo link para o qual o novo elemento será atribuído. O caminho é da seguinte maneira:

      `ExampleModelHasElements.ExampleModel/!ExampleModel/.Elements`

   - O outro caminho vincula o novo elemento a elemento existente. A expressão de caminho Especifica a relação de referência e a função à qual o novo elemento será atribuído. Esse caminho é da seguinte maneira:

      `ExampleElementReferencesTargets.Sources`

      Você pode usar a ferramenta de navegação do caminho para criar cada caminho:

      1. Sob **processa mesclagem Criando links nos caminhos**, clique em  **\<Adicionar caminho >**.

      2. Clique na seta suspensa à direita do item de lista. Uma exibição de árvore é exibida.

      3. Expanda os nós na árvore para formar o caminho que você deseja especificar.

5. Teste o DSL:

   1.  Pressione **F5** para recompilar e executar a solução.

        Recriando levará mais tempo do que o normal porque o código gerado será atualizado a partir de modelos de texto em conformidade com a nova definição de DSL.

   2.  Quando a instância experimental do Visual Studio for iniciado, abra um arquivo de modelo de sua DSL. Crie alguns elementos de exemplo.

   3.  Arraste o **elemento de exemplo** ferramenta em uma forma existente.

        Uma nova forma é exibido e ele está vinculado a forma com um conector existente.

   4.  Copie uma forma existente. Selecione outra forma e colar.

        Uma cópia da primeira forma é criada.  Ele tem um novo nome e ele está vinculado a segunda forma com um conector.

Observe os seguintes pontos deste procedimento:

-   Criando diretivas de mesclagem de elementos, você pode permitir que qualquer classe de elemento para aceitar qualquer outro. O EMD é criado na classe do receptor do domínio e a classe de domínio aceito é especificada na **classe Index** campo.

-   Ao definir caminhos, você pode especificar quais links deve ser usado para conectar o novo elemento ao modelo existente.

     Os links que você especificar deve incluir uma relação de incorporação.

-   O EMD afeta a criação da caixa de ferramentas e também operações de colagem.

     Se você escrever código personalizado que cria novos elementos, você pode invocar explicitamente o EMD usando o `ElementOperations.Merge` método. Isso garante que seu código vincula novos elementos no modelo da mesma forma como outras operações. Para obter mais informações, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).

## <a name="example-adding-custom-accept-code-to-an-emd"></a>Exemplo: Adicionar código de aceitação personalizada a uma EMD

Adicionando código personalizado a uma EMD, você pode definir o comportamento mais complexo de mesclagem. Neste exemplo simples impede que o usuário adicionando mais de um número fixo de elementos no diagrama. O exemplo modifica o padrão EMD que acompanha uma relação de incorporação.

### <a name="to-write-custom-accept-code-to-restrict-what-the-user-can-add"></a>Escrever código aceitação personalizada para restringir o que o usuário pode adicionar

1.  Criar uma DSL usando o **linguagem mínima** modelo de solução. Abra o diagrama de definição de DSL.

2.  No DSL Explorer, expanda **Classes de domínio**, `ExampleModel`, **diretivas de mesclagem de elementos**. Selecione a diretiva element merge chamado `ExampleElement`.

     Este EMD controla como o usuário pode criar novos `ExampleElement` objetos no modelo, por exemplo, arrastando da caixa de ferramentas.

3.  No **detalhes de DSL** janela, selecione **aceitação personalizada usa**.

4.  Recompile a solução. Isso levará mais tempo porque o código gerado será atualizado do modelo.

     Um erro de compilação será relatado, semelhante a: "Company.ElementMergeSample.ExampleElement não contém uma definição para CanMergeExampleElement..."

     Você deve implementar o método `CanMergeExampleElement`.

5.  Criar um novo arquivo de código na **Dsl** projeto. Substitua seu conteúdo pelo código a seguir e altere o namespace para o namespace do seu projeto.

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

    Este exemplo simple restringe o número de elementos que podem ser mescladas no modelo pai. Para condições mais interessantes, o método pode inspecionar qualquer uma das propriedades e links do objeto de recebimento. Ele também pode inspecionar as propriedades dos elementos de mesclagem, que são executadas em um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>. Para obter mais informações sobre `ElementGroupPrototypes`, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md). Para obter mais informações sobre como escrever código que lê um modelo, consulte [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

6.  Teste o DSL:

    1.  Pressione **F5** para recompilar a solução. Quando a instância experimental do Visual Studio é aberto, abra uma instância de sua DSL.

    2.  Crie novos elementos de várias maneiras:

        - Arraste o **elemento de exemplo** ferramenta para o diagrama.

        - No **Gerenciador de modelos de exemplo**, clique com botão direito no nó raiz e, em seguida, clique em **adicionar novo elemento de exemplo**.

        - Copie e cole um elemento no diagrama.

    3.  Verifique se que você não pode usar qualquer uma das seguintes maneiras para adicionar mais de quatro elementos ao modelo. Isso ocorre porque todos eles usam a diretiva de mesclagem.

## <a name="example-adding-custom-merge-code-to-an-emd"></a>Exemplo: Adicionar código personalizado de mesclagem para uma EMD

No código personalizado de mesclagem, você pode definir o que acontece quando o usuário arrasta uma ferramenta ou cola em um elemento. Há duas maneiras de definir uma mesclagem personalizada:

1. Definir **usa personalizado mesclar** e forneça o código necessário. O código substitui o código gerado de mesclagem. Use esta opção se você desejar redefinir completamente o que faz a mesclagem.

2. Substituir a `MergeRelate` método e, opcionalmente, o `MergeDisconnect` método. Para fazer isso, você deve definir a **gera derivado duplo** propriedade da classe de domínio. Seu código pode chamar o código gerado de mesclagem na classe base. Use esta opção se você quiser executar operações adicionais após a mesclagem foi executada.

   Essas abordagens afetam apenas as mesclagens que são executadas usando este EMD. Se você quiser afetar todas as maneiras em que o elemento mesclado pode ser criado, uma alternativa é definir um `AddRule` sobre a relação de incorporação e um `DeleteRule` na classe de domínio mesclada. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).

### <a name="to-override-mergerelate"></a>Para substituir MergeRelate

1.  Na definição de DSL, certifique-se de que você definiu o EMD ao qual você deseja adicionar o código. Se você quiser, você pode adicionar caminhos e definir código de aceitação personalizada conforme descrito nas seções anteriores.

2.  No diagrama DslDefinition, selecione a classe de recebimento da mesclagem. Geralmente, é a classe na extremidade de origem de uma relação de incorporação.

     Por exemplo, em uma DSL gerada a partir da solução de linguagem mínima, selecione `ExampleModel`.

3.  No **propriedades** janela, defina **gera derivado duplo** para **verdadeiro**.

4.  Recompile a solução.

5.  Inspecionar o conteúdo do **Dsl\Generated Files\DomainClasses.cs**. Procure métodos chamados `MergeRelate` e examine seu conteúdo. Isso ajudará você a escrever suas próprias versões.

6.  Em um novo arquivo de código, escrever uma classe parcial para a classe de recebimento e substituir o `MergeRelate` método. Lembre-se de chamar o método base. Por exemplo:

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

### <a name="to-write-custom-merge-code"></a>Escrever código personalizado de mesclagem

1. Na **Dsl\Generated Code\DomainClasses.cs**, inspecione os métodos chamados `MergeRelate`. Esses métodos criam links entre um novo elemento e o modelo existente.

    Além disso, inspecionar métodos chamados `MergeDisconnect`. Esses métodos desvincular um elemento do modelo quando ele deve ser excluído.

2. Na **Gerenciador de DSL**, selecione ou crie a diretiva Element Merge que você deseja personalizar. No **detalhes de DSL** janela, defina **usa personalizado mesclar**.

    Quando você definir essa opção, o **processo de mesclagem** e **encaminhar mesclagem** opções serão ignoradas. Seu código é usado em vez disso.

3. Recompile a solução. Ele levará mais tempo do que o normal porque os arquivos de código gerado serão atualizados do modelo.

    Mensagens de erro serão exibida. Clique duas vezes as mensagens de erro para ver as instruções no código gerado. Pedir que você forneça dois métodos, estas instruções `MergeRelate` *YourDomainClass* e `MergeDisconnect` *YourDomainClass*

4. Os métodos de gravação em uma definição de classe parcial em um arquivo separado código. Os exemplos que você inspecionou anteriormente devem sugerir que você precisa.

   Código personalizado de mesclagem não afetará o código que cria objetos e relações diretamente e não afetará outros EMDs. Para certificar-se de que as alterações adicionais são implementadas, independentemente de como o elemento é criado, considere gravar uma `AddRule` e um `DeleteRule` em vez disso. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).

## <a name="redirecting-a-merge-operation"></a>Redirecionando uma operação de mesclagem

Uma diretiva de mesclagem de encaminhamento redireciona o destino de uma operação de mesclagem. Normalmente, o novo destino é o pai de inserção do destino inicial.

Por exemplo, uma DSL que foi criada com o modelo de diagrama de componente, as portas são incorporadas em componentes. As portas são exibidas como pequenas formas na borda de uma forma de componente. O usuário cria portas, arrastando a ferramenta de porta para uma forma de componente. Mas, às vezes, o usuário por engano arrasta a ferramenta de porta para uma porta existente, em vez do componente, e a operação falhará. Isso é um erro comum quando há várias portas existentes. Para ajudar o usuário para evitar essa incômodo, você pode permitir que as portas ser arrastado para uma porta existente, mas a ação redirecionado para o componente pai. A operação funciona como se o elemento de destino foram o componente.

Você pode criar uma diretiva de mesclagem de avanço na solução de modelo de componente. Se você compila e executa a solução original, você deverá ver o que os usuários poderão arrastar qualquer número de **porta de entrada** ou **porta de saída** elementos a partir de **caixa de ferramentas** para um **Componente** elemento. No entanto, eles não poderão arrastar uma porta para uma porta existente. O ponteiro indisponível alertando-o que essa mudança não está habilitada. No entanto, você pode criar uma diretiva de mesclagem de encaminhamento para que uma porta que seja acidentalmente solto em um existente **porta de entrada** é encaminhado para o **componente** elemento.

### <a name="to-create-a-forward-merge-directive"></a>Para criar uma diretiva de mesclagem de encaminhamento

1. Criar um [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] solução usando o modelo do modelo de componente.

2. Exibição de **Gerenciador de DSL** abrindo Dsldefinition.

3. No **Gerenciador de DSL**, expanda **Classes de domínio**.

4. O **ComponentPort** classe de domínio abstrata é a classe base de ambos **InPort** e **OutPort**. Clique com botão direito **ComponentPort** e, em seguida, clique em **adicionar nova diretiva Element Merge**.

    Uma nova **diretiva Element Merge** nó aparece sob o **diretivas de mesclagem de elementos** nó.

5. Selecione o **diretiva Element Merge** nó e abra o **detalhes de DSL** janela.

6. Na lista de classe de indexação, selecione **ComponentPort**.

7. Selecione **encaminhar mesclagem para uma classe de domínio diferentes**.

8. Na lista de seleção de caminho, expanda **ComponentPort**, expanda **ComponentHasPorts**e, em seguida, selecione **componente**.

    O novo caminho deve ser semelhante a esta:

    **ComponentHasPorts.Component/!Component**

9. Salve a solução e, em seguida, transformar os modelos clicando no botão mais à direita na **Gerenciador de soluções** barra de ferramentas.

10. Criar e executar a solução. Uma nova instância do Visual Studio é exibida.

11. Na **Gerenciador de soluções**, abra Sample.mydsl. O diagrama e o **caixa de ferramentas ComponentLanguage** aparecem.

12. Arraste uma **porta de entrada** da **caixa de ferramentas** para outra **porta de entrada.** Em seguida, arraste uma **OutputPort** para um **InputPort** e, em seguida, a outro **OutputPort**.

     Você não deve ver o ponteiro não está disponível e você poderá remover o novo **porta de entrada** em uma existente. Selecione a nova **porta de entrada** e arrastá-lo para outro ponto a **componente**.

## <a name="see-also"></a>Consulte também

- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md)
- [Exemplo de diagramas de circuito DSL](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)