---
title: Criando uma linguagem específica do domínio baseada no Windows Forms
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 57507775a03bcfd0649f4efbf8a7771fefc8e20b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547310"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>Criar uma linguagem específica de domínio baseada em Windows Forms

Você pode usar Windows Forms para exibir o estado de um modelo de DSL (linguagem específica de domínio), em vez de usar um diagrama DSL. Este tópico orienta você pela Associação de um formulário do Windows a uma DSL usando o Visual Studio Visualization and Modeling SDK.

A imagem a seguir mostra uma interface do usuário do Windows Form e o Gerenciador de modelos para uma instância de DSL:

![Instância de DSL no Visual Studio](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>Criar um Windows Forms DSL

O modelo DSL **mínimo do WinForm designer** cria uma DSL mínima que você pode modificar de acordo com seus próprios requisitos.

1. Crie uma DSL a partir do modelo de **designer do WinForm mínimo** .

    Neste tutorial, os seguintes nomes são assumidos:

   | | |
   |-|-|
   | Nome da solução e DSL | FarmApp |
   | Namespace | Company. FarmApp |

2. Experimente o exemplo inicial que o modelo fornece:

   1. Transforme todos os modelos.

   2. Compile e execute o exemplo (**Ctrl** + **F5**).

   3. Na instância experimental do Visual Studio, abra o `Sample` arquivo no projeto de depuração.

        Observe que ele é exibido em um controle de Windows Forms.

        Você também pode ver os elementos do modelo exibidos no Gerenciador.

        Adicione alguns elementos no formulário ou no Gerenciador e observe que eles aparecem na outra exibição.

   Na instância principal do Visual Studio, observe os seguintes pontos sobre a solução de DSL:

- `DslDefinition.dsl`Não contém elementos de diagrama. Isso ocorre porque você não usará diagramas de DSL para exibir modelos de instância dessa DSL. Em vez disso, você associará um formulário do Windows ao modelo e os elementos no formulário exibirão o modelo.

- Além dos `Dsl` `DslPackage` projetos e, a solução contém um terceiro projeto chamado `UI.` projeto de **interface do usuário** contém a definição de um controle de Windows Forms. `DslPackage`depende `UI` e `UI` depende de `Dsl` .

- No `DslPackage` projeto, `UI\DocView.cs` contém o código que exibe o controle de Windows Forms definido no `UI` projeto.

- O `UI` projeto contém um exemplo funcional de um controle de formulário associado à DSL. No entanto, ele não funcionará quando você tiver alterado a definição de DSL. O `UI` projeto contém:

  - Uma classe de Windows Forms chamada `ModelViewControl` .

  - Um arquivo chamado `DataBinding.cs` que contém uma definição parcial adicional de `ModelViewControl` . Para ver seu conteúdo, em **Gerenciador de soluções**, abra o menu de atalho para o arquivo e escolha **Exibir código**.

### <a name="about-the-ui-project"></a>Sobre o projeto de interface do usuário

Ao atualizar o arquivo de definição de DSL para definir sua própria DSL, você precisará atualizar o controle no `UI` projeto para exibir o DSL. Ao contrário `Dsl` dos `DslPackage` projetos e, o `UI` projeto de exemplo não é gerado a partir do `DslDefinitionl.dsl` . Você pode adicionar arquivos. tt para gerar o código, se desejar, embora isso não seja abordado neste passo a passos.

## <a name="update-the-dsl-definition"></a>Atualizar a definição de DSL

A definição de DSL a seguir é usada neste passo a passos.

![DSL&#45;WPF&#45;1](../modeling/media/dsl-wpf-1.png)

1. Abra DslDefinition. DSL no designer de DSL.

2. Excluir o **exemploelement**

3. Renomeie a classe de domínio **ExampleModel** para `Farm` .

     Forneça as propriedades de domínio adicionais nomeadas `Size` do tipo **Int32**e `IsOrganic` do tipo **booliano**.

    > [!NOTE]
    > Se você excluir a classe de domínio raiz e, em seguida, criar uma nova raiz, precisará redefinir a propriedade da classe raiz do editor. No **Gerenciador de DSL**, selecione **Editor**. Em seguida, no janela Propriedades, defina a **classe raiz** como `Farm` .

4. Use a ferramenta de **classe de domínio nomeada** para criar as seguintes classes de domínio:

    - `Field`-Forneça uma propriedade de domínio adicional chamada `Size` .

    - `Animal`-No janela Propriedades, defina **modificador de herança** como **abstrato**.

5. Use a ferramenta de **classe de domínio** para criar as seguintes classes:

    - `Sheep`

    - `Goat`

6. Use a ferramenta de **herança** para fazer `Goat` e `Sheep` herdar do `Animal` .

7. Use a ferramenta de **incorporação** para inserir `Field` e `Animal` abaixo `Farm` .

8. Talvez você queira organizar o diagrama. Para reduzir o número de elementos duplicados, use o comando **trazer subárvore aqui** no menu de atalho dos elementos folha.

9. **Transforme todos os modelos** na barra de ferramentas de Gerenciador de soluções.

10. Compile o projeto **DSL** .

    > [!NOTE]
    > Neste estágio, os outros projetos não serão compilados sem erros. No entanto, desejamos criar o projeto DSL para que seu assembly esteja disponível para o assistente de fonte de dados.

## <a name="update-the-ui-project"></a>Atualizar o projeto de interface do usuário

Agora você pode criar um novo controle de usuário que exibirá as informações armazenadas no modelo DSL. A maneira mais fácil de conectar o controle de usuário ao modelo é por meio de associações de dados. O tipo de adaptador de ligação de dados chamado **ModelingBindingSource** foi projetado especificamente para conectar DSLs a interfaces não VMSDK.

### <a name="define-your-dsl-model-as-a-data-source"></a>Definir seu modelo de DSL como uma fonte de dados

1. No menu **dados** , escolha **mostrar fontes de dados**.

     A janela **Fontes de Dados** é aberta.

     Escolha **Adicionar nova fonte de dados**. O **Assistente de configuração de fonte de dados** é aberto.

2. Escolha **objeto**, **Avançar**.

     Expanda **DSL**, **Company. FarmApp**e selecione **farm**, que é a classe raiz do seu modelo. Escolha **Concluir**.

     No Gerenciador de Soluções, o projeto de **interface do usuário** agora contém **Properties\DataSources\Farm.DataSource**

     As propriedades e relações de sua classe de modelo aparecem na janela fontes de dados.

     ![DslWpf&#45;3](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>Conectar seu modelo a um formulário

1. No projeto de **interface do usuário** , exclua todos os arquivos. cs existentes.

2. Adicione um novo arquivo de **controle de usuário** chamado `FarmControl` ao projeto **da interface do** usuário.

3. Na janela **fontes de dados** , no menu suspenso no **farm**, escolha **detalhes**.

    Deixe as configurações padrão para as outras propriedades.

4. Abra FarmControl.cs no modo de exibição de design.

    Arraste **farm** da janela Data Sources para FarmControl.

    Um conjunto de controles é exibido, um para cada propriedade. As propriedades da relação não geram controles.

5. Exclua **farmBindingNavigator**. Isso também é gerado automaticamente no `FarmControl` Designer, mas não é útil para esse aplicativo.

6. Usando a caixa de ferramentas, crie duas instâncias de **DataGridView**e nomeie-as `AnimalGridView` e `FieldGridView` .

   > [!NOTE]
   > Uma etapa alternativa é arrastar os itens animais e Fields da janela fontes de dados para o controle. Essa ação cria automaticamente grades de dados e associações entre o modo de exibição de grade e a fonte de dados. No entanto, essa associação não funciona corretamente para DSLs. Portanto, é melhor criar manualmente as grades de dados e associações.

7. Se a caixa de ferramentas não contiver a ferramenta **ModelingBindingSource** , adicione-a. No menu de atalho da guia **dados** , escolha **escolher itens**. Na caixa de diálogo **escolher itens da caixa de ferramentas** , selecione **ModelingBindingSource** na guia **.NET Framework** .

8. Usando a caixa de ferramentas, crie duas instâncias de **ModelingBindingSource**e nomeie-as `AnimalBinding` e `FieldBinding` .

9. Defina a propriedade **DataSource** de cada **ModelingBindingSource** como **farmBindingSource**.

     Defina a propriedade **DataMember** como **animais** ou **Fields**.

10. Defina as propriedades **DataSource** de `AnimalGridView` como `AnimalBinding` e de `FieldGridView` para `FieldBinding` .

11. Ajuste o layout do controle de farm para o seu gosto.

    O **ModelingBindingSource** é um adaptador que executa várias funções específicas para DSLs:

- Ele encapsula as atualizações em uma transação do repositório VMSDK.

   Por exemplo, quando o usuário exclui uma linha da grade de exibição de dados, uma associação regular resultaria em uma exceção de transação.

- Isso garante que, quando o usuário selecionar uma linha, a janela Propriedades exibirá as propriedades do elemento de modelo correspondente, em vez da linha de grade de dados.

  ![DslWpf4 ](../modeling/media/dslwpf4.png) esquema de links entre fontes de dados e exibições.

### <a name="complete-the-bindings-to-the-dsl"></a>Concluir as associações para a DSL

1. Adicione o seguinte código em um arquivo de código separado no projeto de **interface do usuário** :

    ```csharp
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace Company.FarmApp
    {
      partial class FarmControl
      {
        public IContainer Components { get { return components; } }

        /// <summary>Binds the WinForms data source to the DSL model.
        /// </summary>
        /// <param name="nodelRoot">The root element of the model.</param>
        public void DataBind(ModelElement modelRoot)
        {
          WinFormsDataBindingHelper.PreInitializeDataSources(this);
          this.farmBindingSource.DataSource = modelRoot;
          WinFormsDataBindingHelper.InitializeDataSources(this);
        }
      }
    }
    ```

2. No projeto **DslPackage** , edite **DslPackage\DocView.tt** para atualizar a seguinte definição de variável:

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="test-the-dsl"></a>Testar a DSL

A solução DSL agora pode ser criada e executada, embora você queira adicionar mais melhorias posteriormente.

1. Compile e execute a solução.

2. Na instância experimental do Visual Studio, abra o arquivo de **exemplo** .

3. No **FarmApp Explorer**, abra o menu de atalho no nó raiz do **farm** e escolha **Adicionar novo pastor**.

     `Goat1`aparece no modo de exibição **animais** .

    > [!WARNING]
    > Você deve usar o menu de atalho no nó do **farm** , não no nó **animais** .

4. Selecione o nó raiz do **farm** e exiba suas propriedades.

     Na exibição de formulário, altere o **nome** ou o **tamanho** do farm.

     Quando você navega para fora de cada campo no formulário, a propriedade correspondente é alterada no janela Propriedades.

## <a name="enhance-the-dsl"></a>Aprimore a DSL

### <a name="make-the-properties-update-immediately"></a>Fazer as propriedades serem atualizadas imediatamente

1. No modo de exibição de design de FarmControl.cs, selecione um campo simples, como nome, tamanho ou isorgânica.

2. No janela Propriedades, expanda **DataBindings** e abra **(avançado)**.

     Na caixa de diálogo **formatação e Associação avançada** , em **modo de atualização da fonte de dados**, escolha **OnPropertyChanged**.

3. Compile e execute a solução.

     Verifique se, quando você altera o conteúdo do campo, a propriedade correspondente do modelo de farm é alterada imediatamente.

### <a name="provide-add-buttons"></a>Fornecer botões Adicionar

1. No modo de exibição de design de FarmControl.cs, use a caixa de ferramentas para criar um botão no formulário.

    Edite o nome e o texto do botão, por exemplo, para `New Sheep` .

2. Abra o código por trás do botão (por exemplo, clicando duas vezes nele).

    Edite-o da seguinte maneira:

   ```csharp
   private void NewSheepButton_Click(object sender, EventArgs e)
   {
     using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
     {
       elementOperations.MergeElementGroup(farm,
         new ElementGroup(new Sheep(farm.Partition)));
       t.Commit();
     }
   }

   // The following code is shared with other add buttons:
   private ElementOperations operationsCache = null;
   private ElementOperations elementOperations
   {
     get
     {
       if (operationsCache == null)
       {
         operationsCache = new ElementOperations(farm.Store, farm.Partition);
       }
       return operationsCache;
     }
   }
   private Farm farm
   {
     get { return this.farmBindingSource.DataSource as Farm; }
   }
   ```

    Você também precisará inserir a seguinte diretiva:

   ```csharp

   using Microsoft.VisualStudio.Modeling;
   ```

3. Adicione botões semelhantes para Goats e campos.

4. Compile e execute a solução.

5. Verifique se o botão novo adiciona um item. O novo item deve aparecer no FarmApp Explorer e no modo de exibição de grade de dados apropriado.

    Você deve ser capaz de editar o nome do elemento no modo de exibição de grade de dados. Você também pode excluí-lo de lá.

   ![DSL&#45;WPF&#45;2](../modeling/media/dsl-wpf-2.png)

### <a name="about-the-code-to-add-an-element"></a>Sobre o código para adicionar um elemento

Para os novos botões de elemento, o código alternativo a seguir é um pouco mais simples.

```csharp
private void NewSheepButton_Click(object sender, EventArgs e)
{
  using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
  {
    farm.Animals.Add(new Sheep(farm.Partition)); ;
    t.Commit();
  }
}
```

No entanto, esse código não define um nome padrão para o novo item. Ele não executa nenhuma mesclagem personalizada que você possa ter definido nas **diretivas de mesclagem de elementos** da DSL e não executa nenhum código de mesclagem personalizado que possa ter sido definido.

Portanto, recomendamos que você use <xref:Microsoft.VisualStudio.Modeling.ElementOperations> para criar novos elementos. Para obter mais informações, consulte [Personalizando a criação e movimentação do elemento](../modeling/customizing-element-creation-and-movement.md).

## <a name="see-also"></a>Confira também

- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Escrever código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
