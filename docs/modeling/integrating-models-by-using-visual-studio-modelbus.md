---
title: Integrando modelos usando o ModelBus
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a222d5f69d19d2891b4aa20239c1874f55a056e0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536936"
---
# <a name="integrate-models-by-using-visual-studio-modelbus"></a>Integrar modelos usando o Visual Studio ModelBus

Visual Studio ModelBus fornece um método para criar links entre modelos e de outras ferramentas em modelos. Por exemplo, é possível vincular modelos de linguagem específica de domínio (DSL) e modelos UML. É possível criar um conjunto integrado de DSLs.

O ModelBus permite criar uma referência exclusiva para um modelo ou um elemento específico dentro de um modelo. Essa referência pode ser armazenada fora do modelo, por exemplo, em um elemento em outro modelo. Quando, em uma ocasião posterior, uma ferramenta desejar obter acesso ao elemento, a infraestrutura do Model Bus carregará o modelo adequado e retornará o elemento. Se desejar, é possível exibir o modelo ao usuário. Se o arquivo não puder ser acessado em seu local anterior, o ModelBus solicitará ao usuário para encontrá-lo. Se o usuário encontrar o arquivo, o ModelBus fixará todas as referências àquele arquivo.

> [!NOTE]
> Na implementação atual do Visual Studio de ModelBus, os modelos vinculados devem ser itens na mesma solução do Visual Studio.

Para obter informações adicionais e código de exemplo, consulte:

- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)

- [SDK de modelagem para Visual Studio](https://www.microsoft.com/download/details.aspx?id=48148)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="providing-access-to-a-dsl"></a><a name="provide"></a>Fornecendo acesso a uma DSL
 Antes de ser possível criar referências do ModelBus para um modelo ou seus elementos, é necessário definir um ModelBusAdapter para a DSL. A maneira mais fácil de fazer isso é usar a extensão de barramento de modelo do Visual Studio, que adiciona comandos à Designer de DSL.

### <a name="to-expose-a-dsl-definition-to-model-bus"></a><a name="expose"></a>Para expor uma definição de DSL para o barramento de modelo

1. Abra o arquivo de definição de DSL. Clique com o botão direito do mouse na superfície de design e clique em **habilitar ModelBus**.

2. Na caixa de diálogo, escolha **eu quero expor essa DSL ao ModelBus**. É possível escolher as duas opções se desejar que essa DSL exponha seus modelos e consuma referências a outras DSLs.

3. Clique em **OK**. Um novo projeto "ModelBusAdapter" é adicionado à solução de DSL.

4. Se desejar acessar a DSL a partir de um modelo de texto, é necessário modificar o AdapterManager.tt no novo projeto. Ignore essa etapa se desejar acessar a DSL a partir de outro código como comandos e manipuladores de eventos. Para obter mais informações, consulte [usando Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md).

   1. Altere a classe base de AdapterManagerBase para [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)).

   2. Próximo ao final do arquivo, insira esse atributo adicional em frente à classe AdapterManager:

       `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

   3. Nas referências do projeto ModelBusAdapter, adicione **Microsoft. VisualStudio. TextTemplating. Modeling. 11.0**.

      Se desejar acessar a DSL a partir de modelos de texto e de outro código, serão necessários dois adaptadores, um modificado e um não modificado.

5. Clique em **transformar todos os modelos**.

6. Recriar a solução.

   Agora é possível para o ModelBus abrir instâncias dessa DSL.

   A pasta `ModelBusAdapters\bin\*` contém os assemblies compilados pelo projeto `Dsl` e o projeto `ModelBusAdapters`. Para referenciar essa DSL a partir de outra DSL, esses assemblies devem ser importados.

### <a name="ensure-that-elements-can-be-referenced"></a>Verifique se os elementos podem ser referenciados

Os adaptadores Visual Studio ModelBus usam o GUID de um elemento para identificá-lo, por padrão. Esses identificadores devem, portanto, ser persistidos no arquivo do modelo.

Para garantir que as IDs de elemento sejam persistidas:

1. Abra o DslDefinition.dsl.

2. No Gerenciador de DSL, expanda **comportamento de serialização XML**e **dados de classe**.

3. Para cada classe para qual deseja criar referências do Model Bus:

    Clique no nó de classe e, na janela Propriedades, verifique se a **ID de serialização** está definida como `true` .

   Como alternativa, se você quiser usar nomes de elementos para identificar elementos em vez de GUIDs, poderá substituir partes dos adaptadores gerados. Substituir os seguintes métodos na classe do adaptador:

- Substituir `GetElementId` para retornar o identificador que deseja usar. Esse método é chamado ao criar referências.

- Substituir `ResolveElementReference` para localizar o elemento correto a partir de uma referência do Model Bus.

## <a name="accessing-a-dsl-from-another-dsl"></a><a name="editRef"></a>Acessando uma DSL de outra DSL

É possível armazenar referências do model bus em uma propriedade de domínio em uma DSL e, é possível gerar código personalizado que as utiliza. Também é possível permitir ao usuário criar uma referência do model bus selecionando um arquivo de modelo e um elemento dentro dele.

Para permitir que uma DSL use referências a outra DSL, você deve primeiro torná-la um *consumidor* de referências de barramento de modelo.

### <a name="to-enable-a-dsl-to-consume-references-to-an-exposed-dsl"></a>Permitir a uma DSL consumir referências para uma DSL exposta

1. No diagrama de definição de DSL, clique com o botão direito do mouse na parte principal do diagrama e, em seguida, clique em **habilitar ModelBus**.

2. Na caixa de diálogo, selecione **desejo habilitar esse modelo para consumir referências de barramento de modelo**.

3. No projeto Dsl da DSL consumidora, inclua os assemblies a seguir às referências do projeto. Você encontrará esses assemblies (arquivos. dll) no diretório ModelBusAdapter\bin \\ * da DSL exposta.

    - O assembly de DSL exposto, por exemplo **Fabrikam.FamilyTree.Dsl.dll**

    - O assembly do adaptador de barramento de modelo exposto, por exemplo **Fabrikam.FamilyTree.ModelBusAdapter.dll**

4. Inclua os assemblies .NET a seguir às referências de projeto do projeto DSL consumidor.

    1. **Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**

    2. **Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0.dll**

### <a name="to-store-a-model-bus-reference-in-a-domain-property"></a>Armazenar uma Referência do Model Bus em uma propriedade de domínio

1. Na Definição de DSL da DSL consumidora, inclua uma propriedade de domínio a uma classe de domínio e defina seu nome.

2. No janela Propriedades, com a propriedade de domínio selecionada, defina **tipo** como `ModelBusReference` .

   Nesse estágio, o código do programa pode definir o valor da propriedade, porém será somente leitura na janela Propriedades.

   É possível permitir aos usuários definirem a propriedade com um editor de referência do ModelBus especializado. Há duas versões deste editor ou *seletor:* uma permite que os usuários escolham um arquivo de modelo e o outro permite que os usuários escolham um arquivo de modelo e um elemento dentro do modelo.

### <a name="to-allow-the-user-to-set-a-model-bus-reference-in-a-domain-property"></a>Permitir ao usuário definir uma Referência do Model Bus em uma propriedade de domínio

1. Clique com o botão direito do mouse na Propriedade Domain e clique em **Editar propriedades específicas do ModelBusReference**. Uma caixa de diálogo é exibida. Este é o *seletor de barramento de modelo*.

2. Selecione o **tipo apropriado de ModelBusReference**: para um modelo ou para um elemento dentro de um modelo.

3. Na cadeia de caracteres de filtro do diálogo do arquivo, insira uma cadeia como `Family Tree files |*.ftree`. Substitua a extensão de arquivo da sua DSL exposta.

4. Ao escolher referenciar um elemento em um modelo, é possível incluir uma lista de tipos que o usuário pode selecionar, por exemplo, Company.FamilyTree.Person.

5. Clique em **OK**e em **transformar todos os modelos** na barra de ferramentas **Gerenciador de soluções** .

    > [!WARNING]
    > Se nenhum modelo ou entidade válida estiver selecionada, o botão OK não terá efeito, mesmo se parecer estar habilitado.

6. Se uma lista de tipos de destino como Company.FamilyTree.Person tiver sido especificada, será necessário incluir uma referência de assembly para o projeto DSL, referenciando o DLL da DSL de destino, por exemplo, Company.FamilyTree.Dsl.dll

### <a name="to-test-a-model-bus-reference"></a>Testar uma Referência do Model Bus

1. Compile a DSL exposta e a consumidora.

2. Execute uma das DSLs em modo experimental pressionando F5 ou CTRL+F5.

3. No projeto de depuração na instância experimental do Visual Studio, adicione arquivos que sejam instâncias de cada DSL.

    > [!NOTE]
    > Visual Studio ModelBus só pode resolver referências a modelos que são itens na mesma solução do Visual Studio. Por exemplo, não é possível criar uma referência para um arquivo de modelo em outra parte do sistema de arquivos.

4. Crie alguns elementos e vínculos na instância da DSL exposta e salve.

5. Abra uma instância da DSL consumidora e selecione um elemento de modelo que possui uma propriedade de referência do Model Bus.

6. Na janela Propriedades, clique duas vezes na propriedade de referência do Model Bus. O diálogo do seletor é exibido.

7. Clique em **procurar** e selecione a instância da DSL exposta.

     O seletor também permitirá escolher um item no modelo, se o tipo específico de elemento da referência do Model Bus foi especificado.

## <a name="creating-references-in-program-code"></a>Criando Referências no Código do Programa

Quando desejar armazenar uma referência para um modelo ou um elemento dentro de um modelo, crie uma `ModelBusReference`. Existem dois tipos de `ModelBusReference`: referências de modelo e referências de elemento.

Para criar uma referência de modelo, você precisa do Adaptadormanager da DSL do qual o modelo é uma instância e do nome do arquivo ou do item de projeto do Visual Studio do modelo.

Para criar uma referência de elemento, é necessário um adaptador para o arquivo de modelo e o elemento ao qual deseja referir.

> [!NOTE]
> Com o Visual Studio ModelBus, você pode criar referências somente para itens na mesma solução do Visual Studio.

### <a name="import-the-exposed-dsl-assemblies"></a>Importe os assemblies da DSL exposta

No projeto consumidor, inclua referências de projeto para a DSL e os assemblies do ModelBusAdapter da DSL exposta.

Por exemplo, suponha que deseja armazenar Referências do ModelBus em elementos de uma DSL de MusicLibrary. As Referências do ModelBus serão referentes aos elementos da DSL de FamilyTree. No projeto de `Dsl` da solução de MusicLibrary, no nó Referências, inclua referências para os seguintes assemblies:

- Fabrikam.FamilyTree.Dsl.dll - a DSL exposta.

- Fabrikam.FamilyTree.ModelBusAdapters.dll - o adaptador do ModelBus da DSL exposta.

- Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0

- Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0

  Esses assemblies podem ser encontrados no projeto do `ModelBusAdapters` da DSL exposta, sob `bin\*`.

  No arquivo de código onde as referências serão criadas, geralmente será necessário importar esses namespaces:

```csharp
// The namespace of the DSL you want to reference:
using Fabrikam.FamilyTree;  // Exposed DSL
using Fabrikam.FamilyTree.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling.Integration;
using System.Linq;
...
```

### <a name="to-create-a-reference-to-a-model"></a>Criar uma referência para um modelo

Para criar uma referência de modelo, acesse o AdapterManager da DSL exposta e use-o para criar uma referência para o modelo. É possível especificar um caminho de arquivo ou um `EnvDTE.ProjectItem`.

No AdapterManager, é possível obter um Adaptador, que fornece acesso a elementos individuais no modelo.

> [!NOTE]
> É necessário descartar um Adaptador após usá-lo. A maneira mais conveniente de fazer isso é com uma instrução `using`. O exemplo a seguir ilustra isto.

```csharp
// The file path of a model instance of the FamilyTree DSL:
string targetModelFile = "TudorFamilyTree.ftree";
// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Get an adapterManager for the target DSL:
FamilyTreeAdapterManager manager =
    (modelbus.GetAdapterManager(FamilyTreeAdapter.AdapterId)
     as FamilyTreeAdapterManager;
// or: (modelBus.FindAdapterManagers(targetModelFile).First())
// or could provide an EnvDTE.ProjectItem

// Create a reference to the target model:
// NOTE: the target model must be a file in this project.
ModelBusReference modelReference =
     manager.CreateReference(targetModelFile);
// or can use an EnvDTE.ProjectItem instead of the filename

// Get the root element of this model:
using (FamilyTreeAdapter adapter =
     modelBus.CreateAdapter(modelReference) as FamilyTreeAdapter)
{
  FamilyTree modelRoot = adapter.ModelRoot;
  // Access elements under the root in the usual way:
  foreach (Person p in modelRoot.Persons) {...}
  // You can create adapters for individual elements:
  ModelBusReference elementReference =
     adapter.GetElementReference(person);
  ...
} // Dispose adapter
```

Se desejar ser capaz de usar a `modelReference` posteriormente, é possível armazená-la em uma propriedade de domínio que possui o Tipo Externo `ModelBusReference`:

```csharp
using Transaction t = this.Store.TransactionManager
    .BeginTransaction("keep reference"))
{
  artist.FamilyTreeReference = modelReference;
  t.Commit();
}
```

Para permitir aos usuários editar essa propriedade de domínio, use o `ModelReferenceEditor` como o parâmetro no atributo Editor. Para obter mais informações, consulte [permitir que o usuário edite uma referência](#editRef).

### <a name="to-create-a-reference-to-an-element"></a>Criar uma referência para um elemento

O adaptador criado para o modelo pode ser usado para criar e resolver referências.

```csharp
// person is an element in the FamilyTree model:
ModelBusReference personReference =
  adapter.GetElementReference(person);
```

Se desejar ser capaz de usar a `elementReference` posteriormente, é possível armazená-la em uma propriedade de domínio que possui o Tipo Externo `ModelBusReference`. Para permitir aos usuários editá-la, use o `ModelElementReferenceEditor` como o parâmetro no atributo Editor. Para obter mais informações, consulte [permitir que o usuário edite uma referência](#editRef).

### <a name="resolving-references"></a>Resolvendo referências

Se possuir uma `ModelBusReference` (MBR) é possível obter o modelo ou o elemento do modelo ao qual se refere. Se o elemento for apresentado em um diagrama ou em outra visualização, é possível abrir a visualização e selecionar o elemento.

É possível criar um adaptador a partir de uma MBR. A partir do adaptador, é possível obter a raiz do modelo. Também é possível resolver MBRs que referem a elementos específicos dentro do modelo.

```csharp
using Microsoft.VisualStudio.Modeling.Integration; ...
ModelBusReference elementReference = ...;

// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Use a model reference or an element reference
// to obtain an adapter for the target model:
using (FamilyTreeAdapter adapter =
   modelBus.CreateAdapter(elementReference) as FamilyTreeAdapter)
   // or CreateAdapter(modelReference)
{
  // Get the root of the model:
  FamilyTree tree = adapter.ModelRoot;

  // Get a model element:
  MyDomainClass mel =
    adapter.ResolveElementReference<MyDomainClass>(elementReference);
  if (mel != null) {...}

  // Get the diagram or other view, if there is one:
  ModelBusView view = adapter.GetDefaultView();
  if (view != null)
  {
   view.Open();
   // Display the diagram:
   view.Show();
   // Attempt to select the shape that presents the element:
   view.SetSelection(elementReference);
  }
} // Dispose the adapter.
```

#### <a name="to-resolve-modelbus-references-in-a-text-template"></a>Para resolver Referências do ModelBus em um Modelo de Texto

1. A DSL que deseja acessar deve possuir um Adaptador do ModelBus configurado para acesso por modelos de texto. Para obter mais informações, consulte [fornecendo acesso a uma DSL](#provide).

2. Geralmente, uma DSL de destino será acessada usando uma Referência do Model Bus (MBR) armazenada em uma DSL de origem. O modelo, portanto, inclui a diretiva da DSL de origem, mais o código para resolver a MBR. Para obter mais informações sobre modelos de texto, consulte [gerando código de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md).

   ```
   <#@ template debug="true" hostspecific="true"
   inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
   <#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
   <#@ output extension=".txt" #>
   <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
   <#@ assembly name = "System.Core" #>
   <#@ assembly name = "Company.CompartmentDragDrop.Dsl.dll" #>
   <#@ assembly name = "Company.CompartmentDragDrop.ModelBusAdapter.dll" #>
   <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
   <#@ import namespace="System.Linq" #>
   <#@ import namespace="Company.CompartmentDragDrop" #>
   <#@ import namespace="Company.CompartmentDragDrop.ModelBusAdapters" #>
   <# // Get source root from directive processor:
     ExampleModel source = this.ExampleModel;
     // This DSL has a MBR in its root:
   using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as ModelBusAdapter)
     {
     ModelBusAdapterManager manager = this.ModelBus.FindAdapterManagers(this.Host.ResolvePath("Sample.compDD1")).FirstOrDefault();
     ModelBusReference modelReference =
       manager.CreateReference(this.Host.ResolvePath("Sample.compDD1"));

     // Get the root element of this model:
     using (CompartmentDragDropAdapter adapter =
        this.ModelBus.CreateAdapter(modelReference) as CompartmentDragDropAdapter)
     {
       ModelRoot root = adapter.ModelRoot;
   #>
   [[<#= root.Name #>]]
   <#
     }
   #>
   ```

   Para obter mais informações e instruções, consulte [usando Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md)

## <a name="serializing-a-modelbusreference"></a>Serialização de uma ModelBusReference

Se desejar armazenar uma `ModelBusReference` (MBR) na forma de uma cadeia de caracteres, é possível serializá-la:

```csharp
string serialized = modelBus.SerializeReference(elementReference);
// Store it anywhere, then get it back again:
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, null);
```

Uma MBR serializada dessa maneira é independente de contexto. Ao usar o Adaptador do Model Bus baseado em arquivo simples, a MBR contém um caminho de arquivo absoluto. Isso é suficiente se os arquivos do modelo de instância nunca serão movidos. No entanto, os arquivos de modelo normalmente serão itens em um projeto do Visual Studio. A expectativa dos usuários é de poder mover o projeto inteiro para diferentes partes do sistema de arquivos. Eles também esperarão poder manter o projeto sob algum controle de origem e abri-lo em diferentes computadores. Os nomes de caminhos devem, portanto, ser serializados em relação ao local do projeto que contém os arquivos.

### <a name="serializing-relative-to-a-specified-file-path"></a>Serialização relativa a um caminho de arquivo especificado

Uma `ModelBusReference` contém um `ReferenceContext`, que é um dicionário no qual é possível armazenar informações como o caminho de arquivo relativo ao qual deve ser serializado.

Serialização relativa a um caminho:

```csharp
elementReference.ReferenceContext.Add(
   ModelBusReferencePropertySerializer.FilePathSaveContextKey,
   currentProjectFilePath);
string serialized = modelBus.SerializeReference(elementReference);
```

Para recuperar a referência da cadeia de caracteres:

```csharp
ReferenceContext context = new ReferenceContext();
context.Add(ModelBusReferencePropertySerializer.FilePathLoadContextKey,
    currentProjectFilePath);
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, context);
```

### <a name="modelbusreferences-created-by-other-adapters"></a>ModelBusReferences criadas por outros Adaptadores
 As informações a seguir são úteis caso desejar criar seu próprio adaptador.

 Uma `ModelBusReference` (MBR) consiste em duas partes: o cabeçalho da MBR, que é desserializado pelo Model Bus e um adaptador específico que é manipulado pelo gerenciador de adaptador específico. Isso permite fornecer seu próprio formato de serialização de adaptador. Por exemplo, é possível referenciar um banco de dados ao invés de um arquivo ou é possível armazenar informações adicionais na referência do adaptador. Seu próprio adaptador pode inserir informações adicionais no `ReferenceContext`.

 Ao desserializar uma MBR, é necessário fornecer um ReferenceContext, que é armazenado no objeto da MBR. Ao serializar uma MBR, o ReferenceContext armazenado é usado pelo adaptador para ajudar a gerar a cadeia de caracteres. A cadeia de caracteres desserializada não contém todas as informações do ReferenceContext. Por exemplo, no adaptador baseado em arquivo simples, o ReferenceContext contém um caminho de arquivo raiz, que não é armazenado na cadeia de caracteres da MBR serializada.

 A MBR é desserializada em dois estágios:

- `ModelBusReferencePropertySerializer`é o serializador padrão que lida com o cabeçalho MBR. Utiliza o recipiente de propriedades do `SerializationContext` da DSL, que é armazenado no `ReferenceContext` usando a chave `ModelBusReferencePropertySerializer.ModelBusLoadContextKey`. Em específico, o `SerializationContext` deverá conter uma instância do `ModelBus`.

- O Adaptador do ModelBus lida com a parte específica do adaptador da MBR. Poderá usar informações adicionais armazenadas no ReferenceContext da MBR. O adaptador simples baseado em arquivo mantém os caminhos de arquivo raiz usando as chaves `FilePathLoadContextKey` e `FilePathSaveContextKey` .

     Uma referência de adaptador em um arquivo de modelo é desserializada apenas quando é usada.

## <a name="to-create-a-model"></a>Criar um Modelo

### <a name="creating-opening-and-editing-a-model"></a>Criando, abrindo e editando um modelo
 O fragmento a seguir é obtido do exemplo de máquina de estado no site do VMSDK. Ilustra o uso de ModelBusReferences para criar e abrir um modelo e para obter o diagrama associado com o modelo.

 Nessa amostra, o nome da DSL de destino é StateMachine. Diversos nomes são derivados desse nome, como o nome da classe do modelo e o nome do ModelBusAdapter.

```csharp
using Fabrikam.StateMachine.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Integration;
using Microsoft.VisualStudio.Modeling.Integration.Shell;
using Microsoft.VisualStudio.Modeling.Shell;
...
// Create a new model.
ModelBusReference modelReference =
   StateMachineAdapterManager    .CreateStateMachineModel(modelName, fileName);
//Keep reference of new model in this model.
using (Transaction t = ...)
{
  myModelElement.ReferenceProperty = modelReference;
  t.Commit();
}
// Get the ModelBus service from Visual Studio.
IModelBus modelBus = Microsoft.VisualStudio.Shell.Package.
    GetGlobalService(typeof(SModelBus)) as IModelBus;
// Get a modelbus adapter on the new model.
ModelBusAdapter modelBusAdapter;
modelBus.TryCreateAdapter(modelReference,
    this.ServiceProvider, out modelBusAdapter);
using (StateMachineAdapter adapter =
      modelBusAdapter as StateMachineAdapter)
{
    if (adapter != null)
    {
        // Obtain a Diagram from the adapter.
        Diagram targetDiagram =
           ((StandardVsModelingDiagramView)
                 adapter.GetDefaultView()
            ).Diagram;

        using (Transaction t =
             targetDiagram.Store.TransactionManager
                .BeginTransaction("Update diagram"))
        {
            DoUpdates(targetDiagram);
            t.Commit();
        }

        // Display the new diagram.
        adapter.GetDefaultView().Show();
    }
}
```

## <a name="validating-references"></a>Validando referências
 O BrokenReferenceDetector testa todas as propriedades de domínio em um Armazenamento que pode conter ModelBusReferences. Ele chama a ação fornecida onde qualquer ação for encontrada. Isso é particularmente útil para métodos de validação. O método de validação a seguir testa o armazenamento em uma tentativa de salvar o modelo e relata referências quebradas na janela de erros:

```csharp
[ValidationMethod(ValidationCategories.Save)]
public void ValidateModelBusReferences(ValidationContext context)
{
  BrokenReferenceDetector.DetectBrokenReferences(this.Store,
    delegate(ModelElement element, // parent of property
             DomainPropertyInfo property, // identifies property
             ModelBusReference reference) // invalid reference
    {
      context.LogError(string.Format(INVALID_REF_FORMAT,
             property.Name,
             referenceState.Name,
             new ModelBusReferenceTypeConverter().
                 ConvertToInvariantString(reference)),
         "Reference",
         element);
      });
}}
private const string INVALID_REF_FORMAT =
    "The '{0}' domain property of ths ReferenceState instance "
  + "named '{1}' contains reference value '{2}' which is invalid";
```

## <a name="actions-performed-by-the-modelbus-extension"></a>Ações realizadas pela Extensão do ModelBus

As informações a seguir não são essenciais mas podem ser úteis caso faça uso extensivo do ModelBus.

A Extensão do ModelBus realiza as alterações a seguir na solução de DSL.

Ao clicar com o botão direito do mouse no diagrama de definição de DSL, clique em **habilitar ModelBus**e selecione **habilitar esta DSL para consumir o ModelBus**:

- No projeto DSL, uma referência é adicionada a **Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**

- Na Definição de DSL, uma referência de Tipo Externo é incluída: `Microsoft.VisualStudio.Modeling.Integration.ModelBusReference`.

   Você pode ver a referência no **Gerenciador de DSL**, em **tipos de domínio**. Para incluir referências de tipo externo manualmente, clique com o botão direito no nó raiz.

- Um novo arquivo de modelo é adicionado, **Dsl\GeneratedCode\ModelBusReferencesSerialization.tt**.

Quando você define o tipo de uma propriedade de domínio como ModelBusReference, clique com o botão direito do mouse na propriedade e clique em **habilitar propriedades específicas de ModelBusReference**:

- Diversos atributos de CLR são incluídos na propriedade do domínio. É possível visualizá-los no campo Atributos Personalizados na janela Propriedades. No **Dsl\GeneratedCode\DomainClasses.cs**, você pode ver os atributos na declaração da propriedade:

  ```csharp
  [System.ComponentModel.TypeConverter(typeof(
  Microsoft.VisualStudio.Modeling.Integration.ModelBusReferenceTypeConverter))]
  [System.ComponentModel.Editor(typeof(
    Microsoft.VisualStudio.Modeling.Integration.Picker
    .ModelReferenceEditor // or ModelElementReferenceEditor
    ), typeof(System.Drawing.Design.UITypeEditor))]
  [Microsoft.VisualStudio.Modeling.Integration.Picker
    .SupplyFileBasedBrowserConfiguration
    ("Choose a model file", "Target model|*.target")]
  ```

Ao clicar com o botão direito do mouse no diagrama de definição de DSL, clique em **habilitar ModelBus**e selecione **expor esta DSL ao ModelBus**:

- Um novo projeto `ModelBusAdapter` é incluído na solução.

- Uma referência para o `ModelBusAdapter` é incluída no projeto do `DslPackage`. `ModelBusAdapter`tem uma referência ao `Dsl` projeto.

- No **DslPackage\source.extention.tt**, `|ModelBusAdapter|` é adicionado como um componente MEF.

## <a name="see-also"></a>Confira também

- [Como abrir um modelo a partir de um arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)
- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Usando o Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md)
