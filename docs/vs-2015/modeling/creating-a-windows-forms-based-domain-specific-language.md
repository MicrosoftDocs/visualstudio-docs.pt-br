---
title: Criando uma linguagem específica de domínio de baseada em formulários do Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 452318ff-8ecf-46d0-8ca0-4013d0cdafaf
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a79ffda3a044424cc863472c32d62228e90cc6fd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942017"
---
# <a name="creating-a-windows-forms-based-domain-specific-language"></a>Criando uma linguagem específica do domínio baseada no Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o Windows Forms para exibir o estado de um modelo de linguagem específica do domínio (DSL), em vez de usar um diagrama DSL. Este tópico explica como um Windows Form de associação a uma DSL, usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK de visualização e modelagem.  

 ![DSL&#45;Wpf&#45;2](../modeling/media/dsl-wpf-2.png "DSL-Wpf-2")  
Uma instância DSL, mostrando uma interface do usuário do Windows Form e o Gerenciador de modelos.  

## <a name="creating-a-windows-forms-dsl"></a>Criação de uma DSL de formulários do Windows  
 O **WinForm Designer mínimo** modelo DSL cria uma DSL mínimo que você pode modificar para atender às suas próprias necessidades.  

#### <a name="to-create-a-minimal-winforms-dsl"></a>Para criar uma DSL WinForms mínima  

1. Criar uma DSL a partir de **WinForm Designer mínimo** modelo.  

    Neste passo a passo, os seguintes nomes são considerados:  


   |                       |                 |
   |-----------------------|-----------------|
   | Nome da solução e DSL |     FarmApp     |
   |       Namespace       | Company.FarmApp |


2. Fazer experiências com o exemplo inicial que o modelo fornece:  

   1.  Transforme todos os modelos.  

   2.  Compilar e executar o exemplo (**CTRL + F5**).  

   3.  Na instância experimental do Visual Studio, abra o `Sample` arquivo no projeto de depuração.  

        Observe que ele é exibido em um controle Windows Forms.  

        Você também pode ver os elementos do modelo exibido no Explorer.  

        Adicionar alguns elementos no formulário ou o Explorer e observe que eles aparecem na exibição de.  

   Na instância principal de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], observe os seguintes pontos sobre a solução DSL:  

-   `DslDefinition.dsl` não contém nenhum elemento de diagrama. Isso ocorre porque você não usará os diagramas DSL para exibir modelos deste DSL instância. Em vez disso, você associará a um formulário do Windows para o modelo e os elementos no formulário exibirá o modelo.  

-   Além de `Dsl` e `DslPackage` projetos, a solução contém um terceiro projeto chamado `UI.` **interface do usuário** projeto contém a definição de um controle Windows Forms. `DslPackage` depende `UI`, e `UI` depende `Dsl`.  

-   No `DslPackage` projeto, `UI\DocView.cs` contém o código que exibe o controle de formulários do Windows que é definido no `UI` projeto.  

-   O `UI` projeto contém um exemplo de funcionamento de um controle de formulário associado a DSL. No entanto, ele não funcionará quando você alterou a definição de DSL. O `UI` projeto contém:  

    -   Uma classe de formulários do Windows chamada `ModelViewControl`.  

    -   Um arquivo chamado `DataBinding.cs` que contém uma definição parcial adicional de `ModelViewControl`. Para ver seu conteúdo, no **Gerenciador de soluções**, abra o menu de atalho para o arquivo e escolha **Exibir código**.  

### <a name="about-the-ui-project"></a>Sobre o projeto de interface do usuário  
 Quando você atualiza o arquivo de definição de DSL para definir seu próprios DSL, você terá de atualizar o controle no `UI` projeto para exibir sua DSL. Ao contrário de `Dsl` e `DslPackage` projetos, o exemplo `UI` projeto não for gerado de `DslDefinitionl.dsl`. Você pode adicionar arquivos. TT para gerar o código se desejar, embora que não seja abordada neste passo a passo.  

## <a name="updating-the-dsl-definition"></a>Atualizando a definição de DSL  
 O seguinte que definição de DSL é usada neste passo a passo.  

 ![DSL&#45;Wpf&#45;1](../modeling/media/dsl-wpf-1.png "DSL-Wpf-1")  

#### <a name="to-update-the-dsl-definition"></a>Para atualizar a definição de DSL  

1.  Abra o Dsldefinition no designer de DSL.  

2.  Excluir **ExampleElement**  

3.  Renomeie o **ExampleModel** classe de domínio `Farm`.  

     Dê a ele propriedades de domínio adicional denominadas `Size` do tipo **Int32**, e `IsOrganic` do tipo **booliano**.  

    > [!NOTE]
    >  Se você excluir a classe de domínio raiz e, em seguida, cria uma nova raiz, você precisará redefinir a propriedade de classe de raiz do Editor. Na **Gerenciador de DSL**, selecione **Editor**. Em seguida, na janela Propriedades, defina **classe raiz** para `Farm`.  

4.  Use o **classe de domínio chamado** ferramenta para criar as seguintes classes de domínio:  

    -   `Field` – Fornecer uma propriedade de domínio adicional denominada `Size`.  

    -   `Animal` – Na janela Propriedades, defina **modificador de herança** à **abstrata**.  

5.  Use o **classe de domínio** ferramenta para criar as classes a seguir:  

    -   `Sheep`  

    -   `Goat`  

6.  Use o **herança** ferramenta para fazer `Goat` e `Sheep` herdam `Animal`.  

7.  Use o **incorporação** ferramenta incorporar `Field` e `Animal` sob `Farm`.  

8.  Você talvez queira organizar o diagrama. Para reduzir o número de elementos duplicados, use o **trazer subárvore aqui** comando no menu de atalho de elementos folha.  

9. **Transformar todos os modelos** na barra de ferramentas do Gerenciador de soluções.  

10. Criar o **Dsl** projeto.  

    > [!NOTE]
    >  Nesse estágio, os outros projetos não serão compilados sem erros. No entanto, queremos compilar o projeto de Dsl, para que seu assembly está disponível para o Assistente de fonte de dados.  

## <a name="updating-the-ui-project"></a>Atualizando o projeto de interface do usuário  
 Agora você pode criar um novo controle de usuário que exibirá as informações que são armazenadas no modelo de DSL. A maneira mais fácil para conectar-se o controle de usuário para o modelo é por meio de associações de dados. Os tipo de adaptador chamado de associação de dados **ModelingBindingSource** foi projetado especificamente para se conectar a DSLs às interfaces não VMSDK.  

#### <a name="to-define-your-dsl-model-as-a-data-source"></a>Para definir seu modelo DSL como uma fonte de dados  

1.  Sobre o **dados** menu, escolha **Show Data Sources**.  

     O **fontes de dados** janela é aberta.  

     Escolher **Add New Data Source**. O **Data Source Configuration Wizard** é aberta.  

2.  Escolher **objeto**, **próxima**.  

     Expandir **Dsl**, **Company.FarmApp**e selecione **Farm**, que é a classe raiz do seu modelo. Escolha **Concluir**.  

     No Gerenciador de soluções, o **IU** agora contém um projeto **Properties\DataSources\Farm.datasource**  

     As propriedades e relacionamentos de sua classe de modelo são exibidos na janela fontes de dados.  

     ![DslWpf&#45;3](../modeling/media/dslwpf-3.png "DslWpf-3")  

#### <a name="to-connect-your-model-to-a-form"></a>Para se conectar a seu modelo a um formulário  

1. No **interface do usuário** do projeto, exclua todos os arquivos. cs existente.  

2. Adicione um novo **controle de usuário** arquivo chamado `FarmControl` para o **interface do usuário** projeto.  

3. No **fontes de dados** janela, no menu suspenso na **Farm**, escolha **detalhes**.  

    Deixe as configurações padrão para as outras propriedades.  

4. Abra FarmControl.cs na exibição de design.  

    Arraste **Farm** da janela fontes de dados para FarmControl.  

    Um conjunto de controles é exibida, um para cada propriedade. As propriedades da relação não geram controles.  

5. Exclua **farmBindingNavigator**. Isso também é gerado automaticamente no `FarmControl` designer, mas não é útil para este aplicativo.  

6. Usando a caixa de ferramentas, crie duas instâncias de **DataGridView**e nomeá-los `AnimalGridView` e `FieldGridView`.  

   > [!NOTE]
   >  É uma etapa de alternativa ao arrastar os itens de animais e campos da janela fontes de dados para o controle. Essa ação cria automaticamente grades de dados e associações entre a exibição de grade e a fonte de dados. No entanto, essa associação não funciona corretamente para DSLs. Portanto, é melhor criar grades de dados e associações manualmente.  

7. Se a caixa de ferramentas não contém o **ModelingBindingSource** ferramenta, adicioná-lo. No menu de atalho do **dados** guia, escolha **escolher itens**. No **Choose Toolbox Items** caixa de diálogo, selecione **ModelingBindingSource** do **guia do .NET Framework**.  

8. Usando a caixa de ferramentas, crie duas instâncias de **ModelingBindingSource**e nomeá-los `AnimalBinding` e `FieldBinding`.  

9. Defina as **fonte de dados** propriedade de cada **ModelingBindingSource** para **farmBindingSource**.  

     Defina as **DataMember** propriedade **animais** ou **campos**.  

10. Defina as **fonte de dados** propriedades de `AnimalGridView` para `AnimalBinding`e de `FieldGridView` para `FieldBinding`.  

11. Ajuste o layout do controle Farm a seu gosto.  

    O **ModelingBindingSource** é um adaptador que executa várias funções que são específicas a DSLs:  

- Ele encapsula as atualizações em uma transação de Store VMSDK.  

   Por exemplo, quando o usuário exclui uma linha de grade do modo de exibição de dados, uma associação regular resultaria em uma exceção de transação.  

- Isso garante que, quando o usuário seleciona uma linha, a janela Propriedades exibe as propriedades do elemento de modelo correspondente, em vez de linha de grade de dados.  

  ![DslWpf4](../modeling/media/dslwpf4.png "DslWpf4")  
  Esquema de links entre fontes de dados e modos de exibição.  

#### <a name="to-complete-the-bindings-to-the-dsl"></a>Para concluir as associações a DSL  

1.  Adicione o seguinte código em um arquivo de código separado na **interface do usuário** projeto:  

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

2.  No **DslPackage** do projeto, edite **DslPackage\DocView.tt** para atualizar a definição de variável a seguir:  

    ```csharp  
    string viewControlTypeName = "FarmControl";  
    ```  

## <a name="testing-the-dsl"></a>Teste o DSL  
 A solução DSL agora pode compilar e executar, embora você talvez queira adicionar ainda mais melhorias mais tarde.  

#### <a name="to-test-the-dsl"></a>Para testar o DSL  

1.  Criar e executar a solução.  

2.  Na instância experimental do Visual Studio, abra o **amostra** arquivo.  

3.  No **FarmApp Explorer**, abra o menu de atalho na **Farm** nó raiz e, em seguida, escolha **adicionar novo cabra**.  

     `Goat1` aparece na **animais** modo de exibição.  

    > [!WARNING]
    >  Você deve usar o menu de atalho na **Farm** nó, não a **animais** nó.  

4.  Selecione o **Farm** nó raiz e exibir suas propriedades.  

     Na exibição de formulário, alterar o **nome** ou **tamanho** do farm.  

     Quando você navegar para fora de cada campo no formulário, as alterações de propriedade correspondentes na janela Propriedades.  

## <a name="enhancing-the-dsl"></a>Aprimorando a DSL  

#### <a name="to-make-the-properties-update-immediately"></a>Para tornar as propriedades de atualização imediatamente  

1.  Na exibição de design de FarmControl.cs, selecione um campo simples, como nome, tamanho ou IsOrganic.  

2.  Na janela Propriedades, expanda **DataBindings** e abra **(Avançado)**.  

     No **formatação e associação avançada** caixa de diálogo, em **modo de atualização de fonte de dados**, escolha **OnPropertyChanged**.  

3.  Criar e executar a solução.  

     Verifique se que quando você altera o conteúdo do campo, a propriedade correspondente das alterações do modelo de Farm imediatamente.  

#### <a name="to-provide-add-buttons"></a>Para fornecer botões de adição  

1. Na exibição de design de FarmControl.cs, use a caixa de ferramentas para criar um botão no formulário.  

    Edite o nome e o texto do botão, por exemplo ao `New Sheep`.  

2. Abra o código por trás do botão (por exemplo, duas vezes nele).  

    Editá-lo da seguinte maneira:  

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

4. Criar e executar a solução.  

5. Verifique se o novo botão adiciona um item. O novo item deve aparecer no FarmApp Explorer e na exibição de grade de dados apropriado.  

    Você deve ser capaz de editar o nome do elemento na exibição de grade de dados. Você também pode excluí-lo a partir daí.  

   ![DSL&#45;Wpf&#45;2](../modeling/media/dsl-wpf-2.png "DSL-Wpf-2")  

### <a name="about-the-code-to-add-an-element"></a>Sobre o código para adicionar um elemento  
 Para os novos botões de elemento, o seguinte código alternativo é um pouco mais simples.  

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

 No entanto, esse código não define um nome padrão para o novo item. Ele não executa qualquer mesclagem personalizada que você possa ter definido na **diretivas de mesclagem de elementos** da DSL, e não executa qualquer código personalizado de mesclagem que possa ter sido definido.  

 Portanto, é recomendável que você use <xref:Microsoft.VisualStudio.Modeling.ElementOperations> para criar novos elementos. Para obter mais informações, consulte [Personalizando a criação de elemento e a movimentação](../modeling/customizing-element-creation-and-movement.md).  

## <a name="see-also"></a>Consulte também  
 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)   
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)   
 [SDK de Modelagem para Visual Studio – linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)



