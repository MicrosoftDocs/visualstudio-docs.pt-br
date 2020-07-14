---
title: Acessando modelos a partir de modelos (templates) de texto
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, accessing models
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a66f160d25ccacbdaaaf2238dfc738ade4a4200f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531463"
---
# <a name="access-models-from-text-templates"></a>Acessar modelos de modelos de texto

Usando modelos de texto, você pode criar arquivos de relatório, arquivos de código-fonte e outros arquivos de texto baseados em modelos de linguagem específicos de domínio. Para obter informações básicas sobre modelos de texto, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md). Os modelos de texto funcionarão no modo experimental quando você estiver Depurando sua DSL e também funcionará em um computador no qual você implantou a DSL.

> [!NOTE]
> Quando você cria uma solução de DSL, os arquivos de exemplo de modelo de texto ** \* . tt** são gerados no projeto de depuração. Quando você alterar os nomes das classes de domínio, esses modelos deixarão de funcionar. No entanto, eles incluem as diretivas básicas de que você precisa e fornecem exemplos que você pode atualizar para corresponder à sua DSL.

 Para acessar um modelo de um modelo de texto:

- Defina a propriedade Inherit da diretiva de modelo para [Microsoft. VisualStudio. TextTemplating. VSHost. ModelingTextTransformation](/previous-versions/bb893209(v=vs.140)). Isso fornece acesso ao repositório.

- Especifique os processadores de diretiva para a DSL que você deseja acessar. Isso carrega os assemblies para a sua DSL para que você possa usar suas classes de domínio, propriedades e relações no código do seu modelo de texto. Ele também carrega o arquivo de modelo que você especificar.

  Um `.tt` arquivo semelhante ao exemplo a seguir é criado no projeto de depuração quando você cria uma nova solução do Visual Studio a partir do modelo de linguagem mínima de DSL.

```
<#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ output extension=".txt" #>
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>

This text will be output directly.

This is the name of the model: <#= this.ModelRoot.Name #>

Here is a list of elements in the model:
<#
  // When you change the DSL Definition, some of the code below may not work.
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {#>
<#= element.Name #>
<#
  }
#>
```

 Observe os seguintes pontos sobre este modelo:

- O modelo pode usar as classes de domínio, as propriedades e as relações que você definiu na definição de DSL.

- O modelo carrega o arquivo de modelo que você especificar na `requires` propriedade.

- Uma propriedade no `this` contém o elemento raiz. A partir daí, seu código pode navegar para outros elementos do modelo. O nome da propriedade geralmente é o mesmo que a classe de domínio raiz de sua DSL. Neste exemplo, é `this.ExampleModel`.

- Embora o idioma no qual os fragmentos de código são gravados seja C#, você pode gerar texto de qualquer tipo. Como alternativa, você pode escrever o código no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] adicionando a propriedade `language="VB"` à `template` diretiva.

- Para depurar o modelo, adicione `debug="true"` à `template` diretiva. O modelo será aberto em outra instância do Visual Studio se ocorrer uma exceção. Se você quiser dividir o depurador em um ponto específico no código, insira a instrução`System.Diagnostics.Debugger.Break();`

   Para obter mais informações, consulte [Depurando um modelo de texto T4](../modeling/debugging-a-t4-text-template.md).

## <a name="about-the-dsl-directive-processor"></a>Sobre o processador de diretivas DSL
 O modelo pode usar as classes de domínio que você definiu em sua definição de DSL. Isso é trazido por uma diretiva que geralmente aparece próximo ao início do modelo. No exemplo anterior, é o seguinte.

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>
```

 O nome da diretiva ( `MyLanguage` , neste exemplo) é derivado do nome de sua DSL. Ele invoca um *processador de diretiva* que é gerado como parte de sua DSL. Você pode encontrar seu código-fonte em **Dsl\GeneratedCode\DirectiveProcessor.cs**.

 O processador de diretivas DSL executa duas tarefas principais:

- Ele insere efetivamente o assembly e importa diretivas para o modelo que faz referência à sua DSL. Isso permite que você use suas classes de domínio no código do modelo.

- Ele carrega o arquivo que você especifica no `requires` parâmetro e define uma propriedade no `this` que se refere ao elemento raiz do modelo carregado.

## <a name="validating-the-model-before-running-the-template"></a>Validando o modelo antes de executar o modelo
 Você pode fazer com que o modelo seja validado antes que o modelo seja executado.

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>
```

 Observe que:

1. Os `filename` `validation` parâmetros e são separados por ";" e não deve haver outros separadores ou espaços.

2. A lista de categorias de validação determina quais métodos de validação serão executados. Várias categorias devem ser separadas com "&#124;" e não deve haver outros separadores ou espaços.

   Se um erro for encontrado, ele será relatado na janela erros e o arquivo de resultado conterá uma mensagem de erro.

## <a name="accessing-multiple-models-from-a-text-template"></a><a name="Multiple"></a>Acessando vários modelos de um modelo de texto

> [!NOTE]
> Esse método permite que você leia vários modelos no mesmo modelo, mas não oferece suporte a referências de ModelBus. Para ler os modelos que são interligados por referências de ModelBus, consulte [usando Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md).

 Se você quiser acessar mais de um modelo do mesmo modelo de texto, deverá chamar o processador de diretiva gerado uma vez para cada modelo. Você deve especificar o nome do arquivo de cada modelo no `requires` parâmetro. Você deve especificar os nomes que deseja usar para a classe de domínio raiz no `provides` parâmetro. Você deve especificar valores diferentes para os `provides` parâmetros em cada uma das chamadas de diretiva. Por exemplo, suponha que você tenha três arquivos de modelo chamados library. xyz, School. xyz e Work. xyz. Para acessá-los do mesmo modelo de texto, você deve escrever três chamadas de diretiva que se assemelham aos seguintes.

```
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>
```

> [!NOTE]
> Este código de exemplo é para uma linguagem baseada no modelo de solução de linguagem mínima.

 Para acessar os modelos em seu modelo de texto, agora você pode escrever um código semelhante ao código no exemplo a seguir.

```csharp
<#
foreach (ExampleElement element in this.LibraryModel.Elements)
...
foreach (ExampleElement element in this.SchoolModel.Elements)
...
foreach (ExampleElement element in this.WorkModel.Elements)
...
#>
```

```vb
<#
For Each element As ExampleElement In Me.LibraryModel.Elements
...
For Each element As ExampleElement In Me.SchoolModel.Elements
...
For Each element As ExampleElement In Me.WorkModel.Elements
...
#>
```

## <a name="loading-models-dynamically"></a>Carregando modelos dinamicamente
 Se você quiser determinar em tempo de execução quais modelos carregar, você pode carregar um arquivo de modelo dinamicamente no código do programa, em vez de usar a diretiva específica de DSL.

 No entanto, uma das funções da diretiva específica a DSL é importar o namespace de DSL, para que o código de modelo possa usar as classes de domínio definidas nesse DSL. Como você não está usando a diretiva, você deve adicionar **\<assembly>** **\<import>** diretivas e para todos os modelos que você pode carregar. Isso é fácil se os modelos diferentes que você pode carregar são todas as instâncias do mesmo DSL.

 Para carregar o arquivo, o método mais eficaz é usar Visual Studio ModelBus. Em um cenário típico, seu modelo de texto usará uma diretiva específica de DSL para carregar o primeiro modelo da maneira usual. Esse modelo deve conter referências ModelBus a outro modelo. Você pode usar ModelBus para abrir o modelo referenciado e acessar um elemento específico. Para obter mais informações, consulte [usando Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md).

 Em um cenário menos comum, talvez você queira abrir um arquivo de modelo para o qual você tem apenas um nome de arquivo e que pode não estar no projeto atual do Visual Studio. Nesse caso, você pode abrir o arquivo usando a técnica descrita em [como: abrir um modelo do arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md).

## <a name="generating-multiple-files-from-a-template"></a>Gerando vários arquivos de um modelo
 Se você quiser gerar vários arquivos, por exemplo, para gerar um arquivo separado para cada elemento em um modelo, há várias abordagens possíveis. Por padrão, apenas um arquivo é produzido de cada arquivo de modelo.

### <a name="splitting-a-long-file"></a>Dividindo um arquivo longo
 Nesse método, você usa um modelo para gerar um único arquivo, separado por um delimitador. Em seguida, você divide o arquivo em suas partes. Há dois modelos, um para gerar o único arquivo e o outro para dividi-lo.

 **Looptemplate. T4** gera o único arquivo longo. Observe que sua extensão de arquivo é ". T4", porque ela não deve ser processada diretamente quando você clica em **transformar todos os modelos**. Esse modelo usa um parâmetro, que especifica a cadeia de caracteres delimitador que separa os segmentos:

```
<#@ template ninherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ parameter name="delimiter" type="System.String" #>
<#@ output extension=".txt" #>
<#@ MyDSL processor="MyDSLDirectiveProcessor" requires="fileName='SampleModel.mydsl1';validation='open|load|save|menu'" #>
<#
  // Create a file segment for each element:
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {
    // First item is the delimiter:
#>
<#= string.Format(delimiter, element.Id) #>

   Element: <#= element.Name #>
<#
   // Here you generate more content derived from the element.
  }
#>
```

 `LoopSplitter.tt`invoca `LoopTemplate.t4` e, em seguida, divide o arquivo resultante em seus segmentos. Observe que esse modelo não precisa ser um modelo de modelagem, pois ele não lê o modelo.

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#@ import namespace="System.Runtime.Remoting.Messaging" #>
<#@ import namespace="System.IO" #>

<#
  // Get the local path:
  string itemTemplatePath = this.Host.ResolvePath("LoopTemplate.t4");
  string dir = Path.GetDirectoryName(itemTemplatePath);

  // Get the template for generating each file:
  string loopTemplate = File.ReadAllText(itemTemplatePath);

  Engine engine = new Engine();

  // Pass parameter to new template:
  string delimiterGuid = Guid.NewGuid().ToString();
  string delimiter = "::::" + delimiterGuid + ":::";
  CallContext.LogicalSetData("delimiter", delimiter + "{0}:::");
  string joinedFiles = engine.ProcessTemplate(loopTemplate, this.Host);

  string [] separateFiles = joinedFiles.Split(new string [] {delimiter}, StringSplitOptions.None);

  foreach (string nameAndFile in separateFiles)
  {
     if (string.IsNullOrWhiteSpace(nameAndFile)) continue;
     string[] parts = nameAndFile.Split(new string[]{":::"}, 2, StringSplitOptions.None);
     if (parts.Length < 2) continue;
#>
 Generate: [<#= dir #>] [<#= parts[0] #>]
<#
     // Generate a file from this item:
     File.WriteAllText(Path.Combine(dir, parts[0] + ".txt"), parts[1]);
  }
#>
```
