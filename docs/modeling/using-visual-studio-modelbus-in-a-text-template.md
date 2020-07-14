---
title: Usar ModelBus em um modelo de texto
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22a6c9cb035637347ffd501b5cf3b1038cd09369
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535935"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>Usando o Visual Studio ModelBus em um modelo de texto

Se você escrever modelos de texto que leiam um modelo que contém referências de Visual Studio ModelBus, talvez queira resolver as referências para acessar os modelos de destino. Nesse caso, você precisa adaptar os modelos de texto e as DSLs (linguagens específicas de domínio) referenciadas:

- A DSL que é o destino das referências deve ter um adaptador ModelBus configurado para acessar de modelos de texto. Se você também acessar a DSL de outro código, o adaptador reconfigurado será necessário além do adaptador ModelBus padrão.

     O Gerenciador de adaptador deve herdar de [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)) e deve ter o atributo `[HostSpecific(HostName)]` .

- O modelo deve herdar de [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140)).

> [!NOTE]
> Se você quiser ler modelos DSL que não contêm referências ModelBus, poderá usar os processadores de diretiva que são gerados em seus projetos DSL. Para obter mais informações, consulte [acessando modelos de modelos de texto](../modeling/accessing-models-from-text-templates.md).

Para obter mais informações sobre modelos de texto, consulte [geração de código em tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

## <a name="create-a-model-bus-adapter-for-access-from-text-templates"></a>Criar um adaptador de barramento de modelo para acessar de modelos de texto

Para resolver uma referência de ModelBus em um modelo de texto, a DSL de destino deve ter um adaptador compatível. Os modelos de texto são executados em um AppDomain separado dos editores de documento do Visual Studio e, portanto, o adaptador precisa carregar o modelo em vez de acessá-lo por meio do DTE.

1. Se a solução de DSL de destino não tiver um projeto **ModelBusAdapter** , crie um usando o assistente de extensão ModelBus:

    1. Baixe e instale a extensão Visual Studio ModelBus, caso ainda não tenha feito isso. Para obter mais informações, consulte [visualização e SDK de modelagem](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/).

    2. Abra o arquivo de definição de DSL. Clique com o botão direito do mouse na superfície de design e clique em **habilitar ModelBus**.

    3. Na caixa de diálogo, selecione **eu quero expor essa DSL ao ModelBus**. Você pode selecionar ambas as opções se quiser que essa DSL exponha seus modelos e consuma referências a outras DSLs.

    4. Clique em **OK**. Um novo projeto "ModelBusAdapter" é adicionado à solução de DSL.

    5. Clique em **transformar todos os modelos**.

    6. Recriar a solução.

2. Se você quiser acessar a DSL a partir de um modelo de texto e de outro código, como o comando, duplique o projeto **ModelBusAdapter** :

    1. No Windows Explorer, copie e cole a pasta que contém **ModelBusAdapter. csproj**.

    2. Renomeie o arquivo de projeto (por exemplo, para **T4ModelBusAdapter. csproj**).

    3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó da solução, aponte para **Adicionar**e clique em **projeto existente**. Localize o novo projeto de adaptador, **T4ModelBusAdapter. csproj**.

    4. Em cada `*.tt` arquivo do novo projeto, altere o namespace.

    5. Clique com o botão direito do mouse no novo projeto no **Gerenciador de soluções** e clique em **Propriedades**. No editor de propriedades, altere os nomes do assembly gerado e o namespace padrão.

    6. No projeto DslPackage, adicione uma referência ao novo projeto de adaptador para que ele tenha referências a ambos os adaptadores.

    7. No DslPackage\source.extension.tt, adicione uma linha que faça referência ao novo projeto de adaptador.

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **Transforme todos os modelos** e recompile a solução. Nenhum erro de compilação deve ocorrer.

3. No novo projeto de adaptador, adicione referências aos seguintes assemblies:

    - Microsoft. VisualStudio. TextTemplating. 11.0
    - Microsoft. VisualStudio. TextTemplating. Modeling. 11.0

4. Em AdapterManager.tt:

    - Altere a declaração de AdapterManagerBase para que ela herde de [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)).

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - Próximo ao final do arquivo, substitua o atributo HostSpecific antes da classe Adaptermanager. Remova a seguinte linha:

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         Insira a seguinte linha:

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         Esse atributo filtra o conjunto de adaptadores que está disponível quando um consumidor ModelBus pesquisa um adaptador.

5. **Transforme todos os modelos** e recompile a solução. Nenhum erro de compilação deve ocorrer.

## <a name="write-a-text-template-that-can-resolve-modelbus-references"></a>Escrever um modelo de texto que possa resolver referências ModelBus

Normalmente, você começa com um modelo que lê e gera arquivos de uma DSL de "origem". Este modelo usa a diretiva que é gerada no projeto de DSL de origem para ler arquivos de modelo de origem da maneira descrita em [acessando modelos de modelos de texto](../modeling/accessing-models-from-text-templates.md). No entanto, a DSL de origem contém referências de ModelBus a uma DSL de "destino". Portanto, você deseja habilitar o código do modelo para resolver as referências e acessar a DSL de destino. Portanto, você deve adaptar o modelo seguindo estas etapas:

- Altere a classe base do modelo para [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140)).

- Incluir `hostspecific="true"` na diretiva de modelo.

- Adicione referências de assembly para a DSL de destino e seu adaptador e para habilitar ModelBus.

- Você não precisa da diretiva que é gerada como parte da DSL de destino.

```
<#@ template debug="true" hostspecific="true" language="C#"
inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
<#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
<#@ output extension=".txt" #>
<#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
<#@ assembly name = "Company.TargetDsl.Dsl.dll" #>
<#@ assembly name = "Company.TargetDsl.T4ModelBusAdapter.dll" #>
<#@ assembly name = "System.Core" #>
<#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
<#@ import namespace="Company.TargetDsl" #>
<#@ import namespace="Company.TargetDsl.T4ModelBusAdapters" #>
<#@ import namespace="System.Linq" #>
<#
  SourceModelRoot source = this.ModelRoot; // Usual access to source model.
  // In the source DSL Definition, the root element has a model reference:
  using (TargetAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as TargetAdapter)
  {if (adapter != null)
   {
      // Get the root of the target model:
      TargetRoot target = adapter.ModelRoot;
    // The source DSL Definition has a class "SourceElement" embedded under the root.
    // (Let's assume they're all in the same model file):
    foreach (SourceElement sourceElement in source.Elements)
    {
      // In the source DSL Definition, each SourceElement has a MBR property:
      ModelBusReference elementReference = sourceElement.ReferenceToTarget;
      // Resolve the target model element:
      TargetElement element = adapter.ResolveElementReference<TargetElement>(elementReference);
#>
     The source <#= sourceElement.Name #> is linked to: <#= element.Name #> in target model: <#= target.Name #>.
<#
    }
  }}
  // Other useful code: this.Host.ResolvePath(filename) gets an absolute filename
  // from a path that is relative to the text template.
#>
```

 Quando esse modelo de texto é executado, a `SourceDsl` diretiva carrega o arquivo `Sample.source` . O modelo pode acessar os elementos desse modelo, a partir de `this.ModelRoot` . O código pode usar as classes de domínio e as propriedades dessa DSL.

 Além disso, o modelo pode resolver referências de ModelBus. Onde as referências apontam para o modelo de destino, as diretivas de assembly permitem que o código use as classes de domínio e as propriedades da DSL desse modelo.

- Se você não usar uma diretiva que é gerada por um projeto DSL, também deverá incluir o seguinte.

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- Use `this.ModelBus` para obter acesso ao ModelBus.

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>Walkthrough: testando um modelo de texto que usa ModelBus
 Neste tutorial, você seguirá estas etapas:

1. Construa duas DSLs. Uma DSL, o *consumidor*, tem uma `ModelBusReference` propriedade que pode se referir à outra DSL, o *provedor*.

2. Crie dois adaptadores ModelBus no provedor: um para acesso por modelos de texto, o outro para código comum.

3. Crie modelos de instância das DSLs em um único projeto experimental.

4. Defina uma propriedade de domínio em um modelo para apontar para o outro modelo.

5. Escreva um manipulador de clique duplo que abra o modelo que é apontado para.

6. Escreva um modelo de texto que possa carregar o primeiro modelo, siga a referência ao outro modelo e leia o outro modelo.

### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>Construa uma DSL que seja acessível ao ModelBus

1. Crie uma nova solução de DSL. Para este exemplo, selecione o modelo de solução de fluxo de tarefas. Defina o nome do idioma como `MBProvider` e a extensão de nome de arquivo como ". forneça".

2. No diagrama de definição de DSL, clique com o botão direito do mouse em uma parte em branco do diagrama que não está próximo da parte superior e, em seguida, clique em **habilitar ModelBus**.

   Se você não vir **habilitar ModelBus**, baixe e instale a extensão VMSDK ModelBus.

3. Na caixa de diálogo **habilitar ModelBus** , selecione **expor essa DSL para o ModelBus**e clique em **OK**.

    Um novo projeto, `ModelBusAdapter` , é adicionado à solução.

Agora você tem uma DSL que pode ser acessada por modelos de texto por meio de ModelBus. As referências a ela podem ser resolvidas no código de comandos, manipuladores de eventos ou regras, todos os quais operam no AppDomain do editor de arquivo de modelo. No entanto, os modelos de texto são executados em um AppDomain separado e não podem acessar um modelo quando ele está sendo editado. Se você quiser acessar as referências de ModelBus para essa DSL de um modelo de texto, deverá ter um ModelBusAdapter separado.

### <a name="create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>Criar um adaptador ModelBus configurado para modelos de texto

1. No explorador de arquivos, copie e cole a pasta que contém *ModelBusAdapter. csproj*.

    Nomeie a pasta **T4ModelBusAdapter**.

    Renomeie o arquivo de projeto *T4ModelBusAdapter. csproj*.

2. Em Gerenciador de Soluções, adicione T4ModelBusAdapter à solução MBProvider. Clique com o botão direito do mouse no nó da solução, aponte para **Adicionar**e clique em **projeto existente**.

3. Clique com o botão direito do mouse no nó do projeto T4ModelBusAdapter e clique em Propriedades. Na janela Propriedades do projeto, altere o **nome do assembly** e o **namespace padrão** para `Company.MBProvider.T4ModelBusAdapters` .

4. Em cada arquivo *. TT em T4ModelBusAdapter, insira "T4" na última parte do namespace, para que a linha se assemelhe ao seguinte.

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. No `DslPackage` projeto, adicione uma referência de projeto a `T4ModelBusAdapter` .

6. Em DslPackage\source.extension.tt, adicione a linha a seguir em `<Content>` .

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. No `T4ModelBusAdapter` projeto, adicione uma referência a: **Microsoft. VisualStudio. TextTemplating. Modeling. 11.0**

8. Abrir T4ModelBusAdapter\AdapterManager.tt:

   1. Altere a classe base de AdapterManagerBase para [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)). Essa parte do arquivo agora se assemelha ao seguinte.

       ```
       namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters
       {
           /// <summary>
           /// Adapter manager base class (double derived pattern) for the <#= dslName #> Designer
           /// </summary>
           public partial class <#= dslName #>AdapterManagerBase
           : Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager
           {
       ```

   2. Próximo ao final do arquivo, insira o atributo adicional a seguir na frente da classe Adaptermanager.

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        O resultado é semelhante ao seguinte.

       ```
       /// <summary>
       /// ModelBus modeling adapter manager for a <#= dslName #>Adapter model adapter
       /// </summary>
       [Mef::Export(typeof(DslIntegration::ModelBusAdapterManager))]
       [Mef::ExportMetadata(DslIntegration::CompositionAttributes.AdapterIdKey,<#= dslName #>Adapter.AdapterId)]
       [DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]
       [Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]
       public partial class <#= dslName #>AdapterManager : <#= dslName #>AdapterManagerBase
       {
       }
       ```

9. Clique em **transformar todos os modelos** na barra de título de Gerenciador de soluções.

10. Pressione **F5**.

11. Verifique se a DSL está funcionando. No projeto experimental, abra `Sample.provider` . Feche a instância experimental do Visual Studio.

    As referências de ModelBus a essa DSL agora podem ser resolvidas em modelos de texto e também em código comum.

### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>Construir uma DSL com uma propriedade de domínio de referência ModelBus

1. Crie uma nova DSL usando o modelo de solução de linguagem mínima. Nomeie o idioma MBConsumer e defina a extensão de nome de arquivo como ". consume".

2. No projeto DSL, adicione uma referência ao assembly de DSL MBProvider. Clique com o botão direito do mouse `MBConsumer\Dsl\References` e clique em **Adicionar referência**. Na guia **procurar** , localize`MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    Isso permite que você crie código que usa a outra DSL. Se você quiser criar referências a várias DSLs, adicione-as também.

3. No diagrama de definição de DSL, clique com o botão direito do mouse no diagrama e clique em **habilitar ModelBus**. Na caixa de diálogo, selecione **habilitar esta DSL para consumir o ModelBus**.

4. Na classe `ExampleElement` , adicione uma nova propriedade de domínio `MBR` e, na janela Propriedades, defina seu tipo como `ModelBusReference` .

5. Clique com o botão direito do mouse na Propriedade Domain no diagrama e clique em **Editar propriedades específicas do ModelBusReference**. Na caixa de diálogo, selecione **um elemento de modelo**.

    Defina o filtro de caixa de diálogo de arquivo como o seguinte.

    `Provider File|*.provide`

    A subcadeia de caracteres após "&#124;" é um filtro para a caixa de diálogo de seleção de arquivo. Você pode defini-lo para permitir qualquer arquivo usando *.\*

    Na lista **tipo de elemento de modelo** , insira os nomes de uma ou mais classes de domínio no provedor DSL (por exemplo, Company. MBProvider. Task). Elas podem ser classes abstratas. Se você deixar a lista em branco, o usuário poderá definir a referência a qualquer elemento.

6. Feche a caixa de diálogo e **transforme todos os modelos**.

   Você criou uma DSL que pode conter referências a elementos em outra DSL.

### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>Criar uma referência de ModelBus para outro arquivo na solução

1. Na solução MBConsumer, pressione CTRL + F5. Uma instância experimental do Visual Studio é aberta no projeto **MBConsumer\Debugging** .

2. Adicione uma cópia de exemplo. forneça ao projeto **MBConsumer\Debugging** . Isso é necessário porque uma referência de ModelBus deve se referir a um arquivo na mesma solução.

   1. Clique com o botão direito do mouse no projeto de depuração, aponte para **Adicionar**e clique em **Item existente**.

   2. Na caixa de diálogo **Adicionar item** , defina o filtro para **todos os arquivos ( \* . \* )**.

   3. Navegue até `MBProvider\Debugging\Sample.provide` e clique em **Adicionar**.

3. Abra `Sample.consume`.

4. Clique em um exemplo de forma e, na janela Propriedades, clique em **[...]** na propriedade MBR. Na caixa de diálogo, clique em **procurar** e selecione `Sample.provide` . Na janela elementos, expanda a tarefa tipo e selecione um dos elementos.

5. Salve o arquivo. (Ainda não feche a instância experimental do Visual Studio.)

   Você criou um modelo que contém uma referência de ModelBus a um elemento em outro modelo.

### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>Resolver uma referência de ModelBus em um modelo de texto

1. Na instância experimental do Visual Studio, abra um arquivo de modelo de texto de exemplo. Defina seu conteúdo da seguinte maneira.

    ```
    <#@ template debug="true" hostspecific="true" language="C#"
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
    <#@ MBConsumer processor="MBConsumerDirectiveProcessor" requires="fileName='Sample.consume'" #>
    <#@ output extension=".txt" #>
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
    <#@ assembly name = "Company.MBProvider.Dsl.dll" #>
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
    <#@ import namespace="Company.MBProvider" #>
    <#
      // Property provided by the Consumer directive processor:
      ExampleModel consumerModel = this.ExampleModel;
      // Iterate through Consumer model, listing the elements:
      foreach (ExampleElement element in consumerModel.Elements)
      {
    #>
       <#= element.Name #>
    <#
        if (element.MBR != null)
      using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(element.MBR))
      {
              // If we allowed multiple types or DSLs in the MBR, discover type here.
        Task task = adapter.ResolveElementReference<Task>(element.MBR);
    #>
            <#= element.Name #> is linked to Task: <#= task==null ? "(null)" : task.Name #>
    <#
          }
      }
    #>

    ```

     Lembre-se também dos seguintes pontos:

    - Os `hostSpecific` `inherits` atributos e da `template` diretiva devem ser definidos.

    - O modelo de consumidor é acessado da maneira usual por meio do processador de diretiva gerado nesse DSL.

    - As diretivas assembly e Import devem ser capazes de acessar ModelBus e os tipos de DSL do provedor.

    - Se você souber que muitos MBRs estão vinculados ao mesmo modelo, é melhor chamar createadapter apenas uma vez.

2. Salve o modelo. Verifique se o arquivo de texto resultante é semelhante ao seguinte.

    ```
    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2
    ```

### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>Resolver uma referência de ModelBus em um manipulador de gestos

1. Feche a instância experimental do Visual Studio, se estiver em execução.

2. Adicione um arquivo chamado *MBConsumer\Dsl\Custom.cs* e defina seu conteúdo como o seguinte:

    ```csharp
    namespace Company.MB2Consume
    {
      using Microsoft.VisualStudio.Modeling.Integration;
      using Company.MB3Provider;

      public partial class ExampleShape
      {
        public override void OnDoubleClick(Microsoft.VisualStudio.Modeling.Diagrams.DiagramPointEventArgs e)
        {
          base.OnDoubleClick(e);
          ExampleElement element = this.ModelElement as ExampleElement;
          if (element.MBR != null)
          {
            IModelBus modelbus = this.Store.GetService(typeof(SModelBus)) as IModelBus;
            using (ModelBusAdapter adapter = modelbus.CreateAdapter(element.MBR))
            {
              Task task = adapter.ResolveElementReference<Task>(element.MBR);
              // Open a window on this model:
              ModelBusView view = adapter.GetDefaultView();
              view.Show();
              view.SetSelection(element.MBR);
            }
          }
        }
      }
    }
    ```

3. Pressione **Ctrl** + **F5**.

4. Na instância experimental do Visual Studio, abra `Debugging\Sample.consume` .

5. Clique duas vezes em uma forma.

    Se você tiver definido o MBR nesse elemento, o modelo referenciado será aberto e o elemento referenciado será selecionado.

## <a name="see-also"></a>Confira também

- [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
