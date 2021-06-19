---
title: Criar uma Linguagem Específica de Domínio baseada no Windows Forms
description: Fornece informações sobre como usar Windows Forms para exibir o estado de um modelo de linguagem específico do domínio.
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 9a77a22b7ed888b28f12154974d735213952899c
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389534"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>Criar uma linguagem Windows Forms baseada em Domain-Specific dados

Você pode usar Windows Forms para exibir o estado de um modelo DSL (linguagem específica do domínio), em vez de usar um diagrama DSL. Este tópico explica como vincular um Windows Form a uma DSL usando o SDK Visual Studio Visualização e Modelagem.

A imagem a seguir mostra uma interface do usuário do Windows Form e o explorador de modelos para uma instância DSL:

![Instância DSL no Visual Studio](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>Criar um Windows Forms DSL

O modelo DSL mínimo do **WinForm Designer** cria uma DSL mínima que você pode modificar para atender aos seus próprios requisitos.

1. Crie uma DSL do modelo **Mínimo do WinForm Designer.**

    Neste passo a passo, os seguintes nomes são presumidos:

    - Solução e nome DSL: `FarmApp`
    - Namespace: `Company.FarmApp`

2. Experimente o exemplo inicial que o modelo fornece:

   1. Transformar Todos os Modelos.

   2. Criar e executar o exemplo (**Ctrl** + **F5**).

   3. Na instância experimental do Visual Studio, abra `Sample` o arquivo no projeto de depuração.

        Observe que ele é exibido em um controle Windows Forms controle.

        Você também pode ver os elementos do modelo exibidos no Explorer.

        Adicione alguns elementos no formulário ou no Explorer e observe que eles aparecem na outra exibição.

   Na instância principal do Visual Studio, observe os seguintes pontos sobre a solução DSL:

- `DslDefinition.dsl` não contém elementos de diagrama. Isso porque você não usará diagramas DSL para exibir modelos de instância dessa DSL. Em vez disso, você vinculará um Windows Form ao modelo e os elementos no formulário exibirão o modelo.

- Além dos projetos e , a solução contém um terceiro projeto chamado projeto de interface do usuário que contém a definição de um `Dsl` `DslPackage` Windows Forms `UI.`  controle. `DslPackage` depende `UI` de e `UI` depende de `Dsl` .

- No `DslPackage` projeto, `UI\DocView.cs` contém o código que exibe o Windows Forms que é definido no `UI` projeto.

- O `UI` projeto contém uma amostra de trabalho de um controle de formulário vinculado à DSL. No entanto, ele não funcionará quando você tiver alterado a definição de DSL. O `UI` projeto contém:

  - Uma Windows Forms chamada `ModelViewControl` .

  - Um arquivo chamado `DataBinding.cs` que contém uma definição parcial adicional de `ModelViewControl` . Para ver seu conteúdo, **no Gerenciador de Soluções**, abra o menu de atalho do arquivo e escolha **Exibir Código**.

### <a name="about-the-ui-project"></a>Sobre o projeto de interface do usuário

Ao atualizar o arquivo de Definição de DSL para definir sua própria DSL, você terá que atualizar o controle no projeto para `UI` exibir a DSL. Ao contrário `Dsl` dos projetos e , o projeto de exemplo não é gerado do `DslPackage` `UI` `DslDefinitionl.dsl` . Você pode adicionar arquivos .tt para gerar o código se quiser, embora isso não seja abordado neste passo a passo.

## <a name="update-the-dsl-definition"></a>Atualizar a definição de DSL

A imagem a seguir é a definição de DSL usada neste passo a passo.

![Definição de DSL](../modeling/media/dsl-wpf-1.png)

1. Abra DslDefinition.dsl no designer DSL.

2. Excluir **ExampleElement**

3. Renomeie a **classe de domínio ExampleModel** como `Farm` .

     Dê a ele propriedades de domínio `Size` adicionais nomeadas do tipo **Int32** e `IsOrganic` do tipo **booliana**.

    > [!NOTE]
    > Se você excluir a classe de domínio raiz e criar uma nova raiz, será preciso redefinir a propriedade Classe Raiz do Editor. No **DSL Explorer,** selecione **Editor**. Em seguida, no janela Propriedades, de definido **Classe Raiz** como `Farm` .

4. Use a **ferramenta Classe de Domínio** Nomeada para criar as seguintes classes de domínio:

    - `Field` - Dê a ela uma propriedade de domínio adicional chamada `Size` .

    - `Animal` - No janela Propriedades, de definido **Modificador de Herança** como **Abstract**.

5. Use a **ferramenta Classe de** Domínio para criar as seguintes classes:

    - `Sheep`

    - `Goat`

6. Use a **ferramenta Herança** para fazer e herdar `Goat` de `Sheep` `Animal` .

7. Use a **ferramenta De incorporação** para inserir `Field` e em `Animal` `Farm` .

8. Talvez você queira organizar o diagrama. Para reduzir o número de elementos duplicados, use o **comando Bring Subtree Here** no menu de atalho de elementos folha.

9. **Transforme Todos os Modelos** na barra de ferramentas Gerenciador de Soluções.

10. Crie o **projeto Dsl.**

    > [!NOTE]
    > Neste estágio, os outros projetos não serão construídos sem erros. No entanto, queremos criar o projeto Dsl para que seu assembly seja disponibilizado para o Assistente de Fonte de Dados.

## <a name="update-the-ui-project"></a>Atualizar o projeto de interface do usuário

Agora você pode criar um novo controle de usuário que exibirá as informações armazenadas no modelo DSL. A maneira mais fácil de conectar o controle de usuário ao modelo é por meio de vinculações de dados. O tipo de adaptador de associação de dados chamado **ModelingBindingSource** foi projetado especificamente para conectar DSLs a interfaces não VMSDK.

### <a name="define-your-dsl-model-as-a-data-source"></a>Definir seu modelo DSL como uma fonte de dados

1. No menu **Dados,** escolha Mostrar **Fontes de Dados**.

     A janela **Fontes de Dados** é aberta.

     Escolha **Adicionar Nova Fonte de Dados**. O **Assistente de Configuração da Fonte de Dados** é aberto.

2. Escolha **Objeto**, **Próximo**.

     Expanda **Dsl**, **Company.FarmApp** e selecione **Farm**, que é a classe raiz do seu modelo. Escolha **Concluir**.

     No Gerenciador de Soluções, o **projeto de interface** do usuário agora contém **Properties\DataSources\Farm.datasource**

     As propriedades e as relações da classe de modelo aparecem na janela Fontes de Dados.

     ![Janela Fontes de dados](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>Conectar seu modelo a um formulário

1. No projeto **de interface do** usuário, exclua todos os arquivos .cs existentes.

2. Adicione um novo arquivo **de Controle de** Usuário chamado ao projeto de interface `FarmControl` **do** usuário.

3. Na janela **Fontes de** Dados, no menu suspenso do **Farm,** escolha **Detalhes.**

    Deixe as configurações padrão para as outras propriedades.

4. Abra FarmControl.cs na exibição de design.

    Arraste **Farm** da janela Fontes de Dados para FarmControl.

    Um conjunto de controles é exibido, um para cada propriedade. As propriedades de relação não geram controles.

5. **Exclua farmBindingNavigator.** Isso também é gerado automaticamente no `FarmControl` designer, mas não é útil para esse aplicativo.

6. Usando a caixa de ferramentas, crie duas instâncias **de DataGridView** e nomee-as `AnimalGridView` como e `FieldGridView` .

   > [!NOTE]
   > Uma etapa alternativa é arrastar os itens Animais e Campos da janela Fontes de Dados para o controle . Essa ação cria automaticamente grades de dados e vinculações entre a exibição de grade e a fonte de dados. No entanto, essa associação não funciona corretamente para DSLs. Portanto, é melhor criar as grades de dados e as vinculações manualmente.

7. Se a Caixa de Ferramentas não contém a **ferramenta ModelingBindingSource,** adicione-a. No menu de atalho da **guia Dados,** escolha **Escolher Itens**. Na caixa **de diálogo Escolher Itens da** Caixa de Ferramentas, selecione **ModelingBindingSource** na **.NET Framework** guia.

8. Usando a Caixa de Ferramentas, crie duas instâncias **de ModelingBindingSource** e nomee-as `AnimalBinding` como e `FieldBinding` .

9. De definir **a propriedade DataSource** de **cada ModelingBindingSource** como **farmBindingSource.**

     De definir **a propriedade DataMember** como **Animais** ou **Campos**.

10. De definir **as propriedades dataSource** `AnimalGridView` de como e de como `AnimalBinding`  `FieldGridView` `FieldBinding` .

11. Ajuste o layout do controle Farm ao seu gosto.

    O **ModelingBindingSource** é um adaptador que executa várias funções específicas para DSLs:

- Ele envolve atualizações em uma transação do VMSDK Store.

   Por exemplo, quando o usuário exclui uma linha da grade de exibição de dados, uma associação regular resultaria em uma exceção de transação.

- Isso garante que, quando o usuário selecionar uma linha, a janela Propriedades exibirá as propriedades do elemento de modelo correspondente, em vez da linha de grade de dados.

  ![Esquema da Associação DSL](../modeling/media/dslwpf4.png)
  
  Esquema de links entre fontes de dados e exibições.

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

     `Goat1` aparece no modo de exibição **animais** .

    > [!WARNING]
    > Você deve usar o menu de atalho no nó do **farm** , não no nó **animais** .

4. Selecione o nó raiz do **farm** e exiba suas propriedades.

     Na exibição de formulário, altere o **nome** ou o **tamanho** do farm.

     Quando você navega para fora de cada campo no formulário, a propriedade correspondente é alterada no janela Propriedades.

## <a name="enhance-the-dsl"></a>Aprimore a DSL

### <a name="make-the-properties-update-immediately"></a>Fazer as propriedades serem atualizadas imediatamente

1. No modo de exibição de design de FarmControl. cs, selecione um campo simples, como nome, tamanho ou isorgânica.

2. No janela Propriedades, expanda **DataBindings** e abra **(avançado)**.

     Na caixa de diálogo **formatação e Associação avançada** , em **modo de atualização da fonte de dados**, escolha **OnPropertyChanged**.

3. Compile e execute a solução.

     Verifique se, quando você altera o conteúdo do campo, a propriedade correspondente do modelo de farm é alterada imediatamente.

### <a name="provide-add-buttons"></a>Fornecer botões Adicionar

1. No modo de exibição de design de FarmControl. cs, use a caixa de ferramentas para criar um botão no formulário.

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

   ![Exibição de grade de dados de exemplo](../modeling/media/dsl-wpf-2.png)

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

- [Como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md)
- [Escrever código para personalizar um idioma de Domain-Specific](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
