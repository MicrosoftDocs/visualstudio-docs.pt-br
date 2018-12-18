---
title: Usar o ModelBus em um modelo de texto
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 8aed2920e7be177fdbccc9b71796e58cf103e846
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53057581"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>Usando o Visual Studio ModelBus em um modelo de texto
Se você gravar modelos de texto que ler um modelo que contém referências do ModelBus do Visual Studio, você talvez queira resolver as referências para acessar os modelos de destino. Nesse caso, você deve adaptar os modelos de texto e as linguagens específicas de domínio referenciadas (DSLs):

-   O que é o destino das referências de DSL deve ter um adaptador do ModelBus configurado para acesso a partir de modelos de texto. Se você também pode acessar a DSL em outro código, o adaptador reconfigurado é necessário além do padrão adaptador do ModelBus.

     O Gerenciador de adaptador deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager> e deve ter o atributo `[HostSpecific(HostName)]`.

-   O modelo deve herdar de <xref:Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation>.

> [!NOTE]
>  Se você quiser ler modelos DSL que não contêm referências do ModelBus, você pode usar os processadores de diretiva que são gerados em seus projetos DSL. Para obter mais informações, consulte [acessando modelos a partir de modelos de texto](../modeling/accessing-models-from-text-templates.md).

 Para obter mais informações sobre modelos de texto, consulte [geração de código de tempo de Design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

## <a name="creating-a-model-bus-adapter-for-access-from-text-templates"></a>Criando um adaptador de barramento do modelo para acesso a partir de modelos de texto
 Para resolver uma referência do ModelBus em um modelo de texto, DSL de destino deve ter um adaptador compatível. Modelos de texto é executado em um AppDomain separado dos editores de documento do Visual Studio e, portanto, o adaptador tem que carregar o modelo em vez de acessá-lo por meio do DTE.

#### <a name="to-create-a-modelbus-adapter-that-is-compatible-with-text-templates"></a>Para criar um adaptador do ModelBus é compatível com modelos de texto

1.  Se a solução DSL de destino não possui um **ModelBusAdapter** de projeto, crie uma usando o Assistente de extensão do Modelbus:

    1.  Baixe e instale a extensão do ModelBus Visual Studio, se você ainda não tiver feito isso. Para obter mais informações, consulte [SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=185579).

    2.  Abra o arquivo de definição de DSL. Clique duas vezes na superfície de design e, em seguida, clique em **habilitar Modelbus**.

    3.  Na caixa de diálogo, selecione **desejo expor essa DSL ao ModelBus**. Você pode selecionar as duas opções, se você quiser que essa DSL exponha seus modelos e consuma referências a outras DSLs.

    4.  Clique em **OK**. Um novo projeto "ModelBusAdapter" é adicionado à solução de DSL.

    5.  Clique em **transformar todos os modelos**.

    6.  Recompile a solução.

2.  Se você quiser acessar a DSL a partir de um modelo de texto e de outro código, como o comando, duplicar o **ModelBusAdapter** projeto:

    1.  No Windows Explorer, copie e cole a pasta que contém **ModelBusAdapter.csproj**.

    2.  Renomeie o arquivo de projeto (por exemplo, para **T4ModelBusAdapter.csproj**).

    3.  Na **Gerenciador de soluções**, clique com botão direito no nó da solução, aponte para **Add**e, em seguida, clique em **projeto existente**. Localize o novo projeto de adaptador **T4ModelBusAdapter.csproj**.

    4.  Em cada `*.tt` arquivo do novo projeto, altere o namespace.

    5.  Clique com botão direito no novo projeto no Gerenciador de soluções e, em seguida, clique em Propriedades. No editor de propriedades, altere os nomes de assembly gerado e o namespace padrão.

    6.  No projeto DslPackage, adicione uma referência para o novo projeto do adaptador para que ele tenha referências aos dois adaptadores.

    7.  No DslPackage\source.extension.tt, adicione uma linha que faz referência a seu novo projeto do adaptador.

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8.  **Transformar todos os modelos** e recompile a solução. Nenhum erro de compilação deve ocorrer.

3.  No novo projeto do adaptador, adicione referências aos assemblies a seguir:

    -   Microsoft.VisualStudio.TextTemplating.11.0

         Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4.  No AdapterManager.tt:

    -   Altere a declaração do AdapterManagerBase para que ele herda <xref:Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager>.

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    -   No final do arquivo, substitua o atributo HostSpecific antes da classe AdapterManager. Remova a seguinte linha:

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         Insira a seguinte linha:

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         Esse atributo filtra o conjunto de adaptadores que está disponível quando a pesquisa de um consumidor do modelbus para um adaptador.

5.  **Transformar todos os modelos** e recompile a solução. Nenhum erro de compilação deve ocorrer.

## <a name="writing-a-text-template-that-can-resolve-modelbus-references"></a>Gravando um modelo de texto que pode resolver referências do ModelBus
 Normalmente, você começará com um modelo que lê e gera arquivos de uma DSL "origem". Este modelo usa a diretiva que é gerada no projeto DSL de origem para ler arquivos de modelo de origem da maneira que é descrito em [acessando modelos a partir de modelos de texto](../modeling/accessing-models-from-text-templates.md). No entanto, a DSL de origem contém referências do ModelBus para um DSL "target". Portanto, você deseja habilitar o código de modelo resolver as referências e acessar a DSL de destino. Você deve, portanto, adaptar o modelo seguindo estas etapas:

-   Altere a classe base do modelo a ser <xref:Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation>.

-   Incluir `hostspecific="true"` na diretiva do modelo.

-   Adicione referências de assembly para DSL de destino e seu adaptador e para habilitar ModelBus.

-   A diretiva que é gerada como parte da DSL de destino não é necessário.

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

 Quando esse modelo de texto é executado, o `SourceDsl` diretiva carrega o arquivo `Sample.source`. O modelo pode acessar os elementos de modelo, a partir `this.ModelRoot`. O código pode usar as classes de domínio e propriedades dessa DSL.

 Além disso, o modelo pode resolver referências do ModelBus. Em que as referências apontam para o modelo de destino, as diretivas de assembly permitem que o código use as classes de domínio e propriedades de DSL do modelo.

-   Se você não usar uma diretiva que é gerada por um projeto DSL, você também deve incluir o seguinte.

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

-   Use `this.ModelBus` para obter acesso ao ModelBus.

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>Passo a passo: Testando um modelo de texto que usa o ModelBus
 Neste passo a passo, você deve seguir estas etapas:

1.  Construa as duas DSLs. Uma DSL, o *consumidor*, tem um `ModelBusReference` propriedade que pode se referir a DSL, o *provedor*.

2.  Crie dois adaptadores do ModelBus no provedor: uma para acesso por modelos de texto, o outro para um código comum.

3.  Crie modelos de instância das DSLs em um único projeto experimental.

4.  Defina uma propriedade de domínio em um modelo para apontar para outro modelo.

5.  Escreva um manipulador de clique duplo que abre o modelo que é apontado.

6.  Escreva um modelo de texto que pode carregar o primeiro modelo, siga a referência a outro modelo e outro modelo de leitura.

#### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>Construir uma DSL que seja acessível ao ModelBus

1. Crie uma nova solução DSL. Neste exemplo, selecione o modelo de solução de fluxo de tarefa. Defina o nome de idioma como `MBProvider` e a extensão de nome de arquivo para ".provide".

2. No diagrama de definição de DSL, uma parte em branco do diagrama que não está na parte superior com o botão direito e, em seguida, clique em **habilitar Modelbus**.

   -   Se você não vir **habilitar Modelbus**, você deve baixar e instalar a extensão do ModelBus VMSDK. Encontrá-lo no site do VMSDK: [SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=185579).

3. No **habilitar Modelbus** caixa de diálogo, selecione **expor essa DSL ao ModelBus**e, em seguida, clique em **Okey**.

    Um novo projeto, `ModelBusAdapter`, é adicionado à solução.

   Agora você tem uma DSL que pode ser acessada por modelos de texto por meio do ModelBus. Referências a ele podem ser resolvidas no código de comandos, manipuladores de eventos ou regras, que operam no AppDomain do editor de arquivo de modelo. No entanto, os modelos de texto executar em um AppDomain separado e não podem acessar um modelo quando ele está sendo editado. Se você quiser acessar referências do ModelBus para esta DSL a partir de um modelo de texto, você deve ter um ModelBusAdapter separado.

#### <a name="to-create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>Para criar um adaptador do ModelBus configurado para modelos de texto

1. No Windows Explorer, copie e cole a pasta que contém ModelBusAdapter.csproj.

    Nomeie a pasta T4ModelBusAdapter.

    Renomeie o arquivo de projeto T4ModelBusAdapter.csproj.

2. No Gerenciador de soluções, adicione T4ModelBusAdapter à solução MBProvider. Clique com botão direito no nó da solução, aponte para **Add**e, em seguida, clique em **projeto existente**.

3. Clique com botão direito no nó do projeto T4ModelBusAdapter e, em seguida, clique em Propriedades. Na janela de propriedades do projeto, altere a **nome do Assembly** e **Namespace padrão** para `Company.MBProvider.T4ModelBusAdapters`.

4. Em cada arquivo TT no T4ModelBusAdapter, insira "T4" na última parte do namespace, para que a linha é semelhante à seguinte.

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. No `DslPackage` do projeto, adicione uma referência de projeto para `T4ModelBusAdapter`.

6. No DslPackage\source.extension.tt, adicione a seguinte linha em `<Content>`.

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. No `T4ModelBusAdapter` do projeto, adicione uma referência a: **Microsoft.VisualStudio.TextTemplating.Modeling.11.0**

8. Abra T4ModelBusAdapter\AdapterManager.tt:

   1.  Altere a classe base do AdapterManagerBase para <xref:Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager>. Esta parte do arquivo agora é semelhante à seguinte.

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

   2.  No final do arquivo, insira o seguinte atributo adicional em frente à classe AdapterManager.

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        O resultado é semelhante à seguinte.

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

9. Clique em **transformar todos os modelos** na barra de título do Solution Explorer.

10. Recompile a solução. Clique em F5.

11. Verifique se a DSL está funcionando pressionando F5. No projeto experimental, abra `Sample.provider`. Feche a instância experimental do Visual Studio.

    Referências do ModelBus para esta DSL agora podem ser resolvidas em modelos de texto e também em código comum.

#### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>Construir uma DSL com uma propriedade de domínio de referência do ModelBus

1. Crie uma nova DSL usando o modelo de solução de linguagem mínima. Nomeie a linguagem MBConsumer e definir a extensão de nome de arquivo para ".consume".

2. No projeto DSL, adicione uma referência ao assembly MBProvider DSL. Clique com botão direito `MBConsumer\Dsl\References` e, em seguida, clique em **adicionar referência**. No **procurar** guia, localize `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll`

    Isso permite que você crie código que usa outro DSL. Se você quiser criar referências para diversas DSLs, adicioná-los também.

3. No diagrama de definição de DSL, clique com botão direito do diagrama e, em seguida, clique em **habilitar ModelBus**. Na caixa de diálogo, selecione **habilitar esta DSL consumir o ModelBus**.

4. Na classe `ExampleElement`, adicione uma nova propriedade de domínio `MBR`e na janela Propriedades, defina seu tipo como `ModelBusReference`.

5. A propriedade de domínio no diagrama com o botão direito e, em seguida, clique em **propriedades específicas da ModelBusReference editar**. Na caixa de diálogo, selecione **um elemento de modelo**.

    Defina o filtro da caixa de diálogo de arquivo como a seguir.

    `Provider File|*.provide`

    A subcadeia de caracteres após o "&#124;" é um filtro para a caixa de diálogo de seleção de arquivo. Você pode defini-lo para permitir que todos os arquivos usando *.\*

    No **tipo de elemento de modelo** lista, insira os nomes de classes de domínio mais de uma ou no provedor de DSL (por exemplo, Company.MBProvider.Task). Eles podem ser classes abstratas. Se você deixar a lista, o usuário pode definir a referência a qualquer elemento.

6. Feche a caixa de diálogo e **transformar todos os modelos**.

   Você criou uma DSL que pode conter referências a elementos em outra DSL.

#### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>Criar uma referência do ModelBus para outro arquivo na solução

1. Na solução MBConsumer, pressione CTRL + F5. Uma instância experimental do Visual Studio é aberto na **MBConsumer\Debugging** projeto.

2. Adicionar uma cópia de Sample.provide para o **MBConsumer\Debugging** projeto. Isso é necessário porque uma referência do ModelBus deve se referir a um arquivo na mesma solução.

   1.  Depuração de projeto com o botão direito, aponte para **Add**e, em seguida, clique em **Item existente**.

   2.  No **Adicionar Item** caixa de diálogo, defina o filtro para **todos os arquivos (\*.\*)** .

   3.  Navegue até `MBProvider\Debugging\Sample.provide` e, em seguida, clique em **Add**.

3. Abra `Sample.consume`.

4. Clique em uma forma de exemplo e, em seguida, na janela Propriedades, clique em **[...]**  na propriedade MBR. Na caixa de diálogo, clique em **navegue** e selecione `Sample.provide`. Na janela de elementos, expanda o tipo de tarefa e selecione um dos elementos.

5. Salve o arquivo.

    (Não ainda feche a instância experimental do Visual Studio.)

   Você criou um modelo que contém uma referência do ModelBus para um elemento em outro modelo.

#### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>Resolver uma referência do ModelBus em um modelo de texto

1.  Na instância experimental do Visual Studio, abra um arquivo de modelo de texto de exemplo. Defina seu conteúdo da seguinte maneira.

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

    1.  O `hostSpecific` e `inherits` atributos do `template` diretiva deve ser definida.

    2.  O modelo de consumidor é acessado da maneira usual por meio do processador de diretriz que foi gerado nessa DSL.

    3.  As diretivas de importação e o assembly devem ser capazes de acessar o ModelBus e os tipos de provedor de DSL.

    4.  Se você souber que muitos MBRs estejam vinculados ao mesmo modelo, é melhor chamar CreateAdapter apenas uma vez.

2.  Salve o modelo. Verifique se que o arquivo de texto resultante é semelhante à seguinte.

    ```

    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2

    ```

#### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>Resolver uma referência do ModelBus em um manipulador de gesto

1.  Feche a instância experimental do Visual Studio, se ele estiver em execução.

2.  Adicione um arquivo que é chamado MBConsumer\Dsl\Custom.cs e defina seu conteúdo para o seguinte.

    ```

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

3.  Pressione CTRL+F5.

4.  Na instância experimental do Visual Studio, abra `Debugging\Sample.consume`.

5.  Clique duas vezes em uma forma.

     Se você tiver definido o MBR nesse elemento, o modelo referenciado é aberto e o elemento referenciado está selecionado.

## <a name="see-also"></a>Consulte também

- [Integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
