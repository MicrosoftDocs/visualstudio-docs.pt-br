---
title: Acessando modelos a partir de modelos de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, accessing models
ms.assetid: cf65395a-0ca3-4826-89c7-b1869562685c
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: f311018197040c0c908964a49f63ab130121c8c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919852"
---
# <a name="accessing-models-from-text-templates"></a>Acessando modelos a partir de modelos (templates) de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando modelos de texto, você pode criar arquivos de relatório, os arquivos de código-fonte e outros arquivos de texto baseados em modelos de linguagem específica do domínio. Para obter informações básicas sobre modelos de texto, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md). Os modelos de texto funcionarão no modo experimental quando você estiver depurando sua DSL e também funcionará em um computador no qual você implantou a DSL.  
  
> [!NOTE]
>  Quando você cria uma solução DSL, o modelo de texto de exemplo  **\*. TT** arquivos são gerados no projeto de depuração. Quando você altera os nomes das classes de domínio, esses modelos não funcionará mais. No entanto, eles incluem as diretivas básicas que você precisa e fornecem exemplos que você pode atualizar para corresponder à sua DSL.  
  
 Para acessar um modelo de um modelo de texto:  
  
- Defina a propriedade de herdar da diretiva do modelo para <xref:Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation>. Isso fornece acesso para a Store.  
  
- Especifique a processadores de diretiva para a DSL que você deseja acessar. Isso carrega os assemblies da DSL para que você possa usar suas classes de domínio, propriedades e relacionamentos no código do modelo de texto. Ele também carrega o arquivo de modelo que você especificar.  
  
  Um `.tt` arquivo semelhante ao exemplo a seguir é criado no projeto de depuração quando você cria um novo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução a partir do modelo de linguagem mínima de DSL.  
  
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
  
-   O modelo pode usar as classes de domínio, propriedades e relações que você definiu na definição de DSL.  
  
-   O modelo carrega o arquivo de modelo que você especificar na `requires` propriedade.  
  
-   Uma propriedade em `this` contém o elemento raiz. A partir daí, seu código pode navegar para outros elementos do modelo. O nome da propriedade normalmente é o mesmo que a classe de domínio raiz de sua DSL. Neste exemplo, é `this.ExampleModel`.  
  
-   Embora o idioma no qual os fragmentos de código são escritos em C#, você pode gerar o texto de qualquer tipo. Como alternativa, você pode escrever o código em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] adicionando a propriedade `language="VB"` para o `template` diretiva.  
  
-   Para depurar o modelo, adicione `debug="true"` para o `template` diretiva. O modelo será aberto em outra instância do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] se ocorrer uma exceção. Se você quiser interromper o depurador em um ponto específico no código, insira a instrução `System.Diagnostics.Debugger.Break();`  
  
     Para obter mais informações, consulte [depurando um modelo de texto T4](../modeling/debugging-a-t4-text-template.md).  
  
## <a name="about-the-dsl-directive-processor"></a>Sobre o processador de diretriz de DSL  
 O modelo pode usar as classes de domínio que você definiu na sua definição de DSL. Isso é causado por uma diretiva que normalmente é exibida no início do modelo. No exemplo anterior, é o seguinte.  
  
```  
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>  
```  
  
 O nome da diretiva ( `MyLanguage`, neste exemplo) é derivado do nome da sua DSL. Ele chama um *processador de diretriz* que é gerado como parte de sua DSL. Você pode encontrar seu código-fonte no **Dsl\GeneratedCode\DirectiveProcessor.cs**.  
  
 O processador de diretriz DSL executa duas tarefas principais:  
  
-   Ele efetivamente insere diretivas de assembly e importar o modelo que faz referência a sua DSL. Isso permite que você use suas classes de domínio no código do modelo.  
  
-   Ele carrega o arquivo que você especificar na `requires` parâmetro e define uma propriedade na `this` que se refere ao elemento raiz do modelo carregado.  
  
## <a name="validating-the-model-before-running-the-template"></a>Validando o modelo antes de executar o modelo  
 Você pode fazer com que o modelo a ser validado antes do modelo é executado.  
  
```  
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>  
  
```  
  
 Observe que:  
  
1. O `filename` e `validation` parâmetros são separados por ";" e não deve haver nenhuma outra separadores ou espaços.  
  
2. A lista de categorias de validação determina quais métodos de validação serão executados. Várias categorias devem ser separadas por "&#124;" e não deve haver nenhuma outra separadores ou espaços.  
  
   Se um erro for encontrado, ele será relatado na janela de erros e o arquivo de resultados conterá uma mensagem de erro.  
  
##  <a name="Multiple"></a> Acessando vários modelos de um modelo de texto  
  
> [!NOTE]
>  Esse método permite que você leia vários modelos no mesmo modelo, mas não oferece suporte a referências do ModelBus. Para ler os modelos que estão interconectados por referências do ModelBus, consulte [usando o Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md).  
  
 Se você deseja acessar mais de um modelo a partir do mesmo modelo de texto, você deve chamar o processador de diretriz gerado uma vez para cada modelo. Você deve especificar o nome do arquivo de cada modelo no `requires` parâmetro. Você deve especificar os nomes que você deseja usar para a classe de domínio raiz no `provides` parâmetro. Você deve especificar valores diferentes para o `provides` parâmetros de cada uma das chamadas de diretiva. Por exemplo, suponha que você tenha três arquivos de modelo chamados Library.xyz, School.xyz e Work.xyz. Para acessá-los a partir do mesmo modelo de texto, você deve escrever três chamadas diretivas semelhantes às seguintes.  
  
```  
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>  
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>  
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>  
```  
  
> [!NOTE]
>  Esse código de exemplo é para um idioma que é baseado no modelo de solução de linguagem mínima.  
  
 Para acessar os modelos em seu modelo de texto, agora você pode escrever código semelhante ao código no exemplo a seguir.  
  
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
 Se você quiser determinar no tempo de execução que modelos para carregar, você pode carregar um arquivo de modelo dinamicamente no código do programa, em vez de usar a diretiva da DSL específicos.  
  
 No entanto, uma das funções da diretiva específica DSL é importar o namespace DSL, para que o código do modelo possa usar as classes de domínio definidas dessa DSL. Porque você não estiver usando a diretiva, você deve adicionar  **\<assembly >** e  **\<Importar >** diretivas para todos os modelos que você pode carregar. Isso é fácil se os modelos diferentes que você pode carregar são todas as instâncias da mesma DSL.  
  
 Para carregar o arquivo, o método mais eficaz é usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus. Em um cenário típico, o modelo de texto será usar uma diretiva de DSL específicas para carregar o modelo primeiro como de costume. Esse modelo conteria referências do ModelBus para outro modelo. Você pode usar o ModelBus abrir o modelo de referência e acessar um elemento específico. Para obter mais informações, consulte [usando o Visual Studio ModelBus em um modelo de texto](../modeling/using-visual-studio-modelbus-in-a-text-template.md).  
  
 Em um cenário menos comum, você talvez queira abrir um arquivo de modelo para os quais você tem apenas um nome de arquivo, e que talvez não seja o atual [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto. Nesse caso, você pode abrir o arquivo usando a técnica descrita [como: abrir um modelo de arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md).  
  
## <a name="generating-multiple-files-from-a-template"></a>Gerar vários arquivos de um modelo  
 Se você quiser gerar um vários arquivos – por exemplo, para gerar um arquivo separado para cada elemento em um modelo, há várias abordagens possíveis. Por padrão, somente um arquivo é produzido a partir de cada arquivo de modelo.  
  
### <a name="splitting-a-long-file"></a>Dividir um arquivo longo  
 Nesse método, você pode usar um modelo para gerar um único arquivo, separado por um delimitador. Em seguida, você deve dividir o arquivo em suas partes. Há dois modelos, uma para gerar o arquivo único e o outro para dividi-la.  
  
 **LoopTemplate.t4** gera o único arquivo longo. Observe que a sua extensão de arquivo é ".t4", porque ele não deve ser processado diretamente quando você clica em **transformar todos os modelos**. Esse modelo tem um parâmetro que especifica a cadeia de caracteres de delimitador que separa os segmentos:  
  
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
  
 `LoopSplitter.tt` invoca `LoopTemplate.t4`e, em seguida, divide o arquivo resultante em seus segmentos. Observe que esse modelo não precisa ser um modelo de modelagem, porque ela não ler o modelo.  
  
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



