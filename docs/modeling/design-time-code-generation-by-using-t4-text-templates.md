---
title: Geração de código na hora de design usando modelos de texto T4
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, guidelines for code generation
- text templates, data source model
- TextTemplatingFileGenerator custom tool
- Transform All Templates
- text templates, getting started
- Text Template project item
- text templates, generating code for your application
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8589be1bd1c1e9ad86a412d4f8bd2630c93a42ac
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535987"
---
# <a name="design-time-code-generation-by-using-t4-text-templates"></a>Geração de código na hora de design usando modelos de texto T4

Modelos de texto T4 de tempo de design permitem gerar código de programa e outros arquivos em seu projeto do Visual Studio. Normalmente, você escreve os modelos para que variem o código que eles geram de acordo com os dados de um *modelo*. Um modelo é um arquivo ou banco de dados que contém informações importantes sobre os requisitos do seu aplicativo.

Por exemplo, você pode ter um modelo que define um fluxo de trabalho, como uma tabela ou um diagrama. A partir do modelo, você pode gerar o software que executa o fluxo de trabalho. Quando os requisitos dos usuários mudam, é fácil discutir o novo fluxo de trabalho com os usuários. Gerar novamente o código do fluxo de trabalho é mais confiável do que atualizar o código manualmente.

> [!NOTE]
> Um *modelo* é uma fonte de dados que descreve um aspecto específico de um aplicativo. Ela pode estar em qualquer formulário, tipo de arquivo ou banco de dados. Ela não precisa estar em qualquer formulário particular, como um modelo UML ou modelo DSL. Os modelos comuns estão na forma de tabelas ou arquivos XML.

Você provavelmente já está familiarizado com a geração de código. Quando você define recursos em um arquivo **. resx** em sua solução do Visual Studio, um conjunto de classes e métodos é gerado automaticamente. O arquivo de recursos torna mais fácil e confiável editar os recursos do que se você tivesse que editar as classes e métodos. Com modelos de texto, você pode gerar o código da mesma forma a partir de uma fonte de seu próprio projeto.

Um modelo de texto contém uma mistura do texto que você deseja gerar e o código de programa que gera partes variáveis ​​do texto. O código do programa permite que você repita ou omita condicionalmente partes do texto gerado. O texto gerado pode ser o próprio código de programa que fará parte do seu aplicativo.

## <a name="create-a-design-time-t4-text-template"></a>Criar um modelo de texto T4 de tempo de design

1. Crie um novo projeto do Visual Studio ou abra um existente.

2. Adicione um arquivo de modelo de texto ao seu projeto e dê a ele um nome que tenha a extensão **. tt**.

    Para fazer isso, em **Gerenciador de soluções**, no menu de atalho do seu projeto, escolha **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , selecione **modelo de texto** no painel central.

    Observe que a propriedade de **ferramenta personalizada** do arquivo é **TextTemplatingFileGenerator**.

3. Abra o arquivo. Ele conterá as seguintes diretrizes:

   ```
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   ```

    Se você adicionou o modelo a um projeto [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], o atributo language será "`VB`".

4. Adicione algum texto no final do arquivo. Por exemplo:

   ```
   Hello, world!
   ```

5. Salve o arquivo.

    Você pode ver uma caixa de mensagem de **aviso de segurança** que solicita que você confirme se deseja executar o modelo. Clique em **OK**.

6. Em **Gerenciador de soluções**, expanda o nó arquivo de modelo e você encontrará um arquivo com a extensão **. txt**. O arquivo contém o texto gerado a partir do modelo.

   > [!NOTE]
   > Se seu projeto for um projeto Visual Basic, você deverá clicar em **Mostrar todos os arquivos** para ver o arquivo de saída.

### <a name="regenerate-the-code"></a>Gerar novamente o código

Um modelo será executado, gerando o arquivo subsidiário, em qualquer um dos seguintes casos:

- Edite o modelo e altere o foco para uma janela diferente do Visual Studio.

- Salve o modelo.

- Clique em **transformar todos os modelos** no menu **Compilar** . Isso irá transformar todos os modelos na solução do Visual Studio.

- No **Gerenciador de soluções**, no menu de atalho de qualquer arquivo, escolha **executar ferramenta personalizada**. Use esse método para transformar um subconjunto de modelos selecionado.

Você também pode configurar um projeto do Visual Studio para que os modelos sejam executados quando os arquivos de dados lidos tiverem sido alterados. Para obter mais informações, consulte [Regenerando o código automaticamente](#Regenerating).

## <a name="generate-variable-text"></a>Gerar texto variável

Os modelos de texto permitem que você use o código de programa para alterar o conteúdo do arquivo gerado.

1. Altere o conteúdo do arquivo `.tt`:

   ```csharp
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   <#int top = 10;

   for (int i = 0; i<=top; i++)
   { #>
      The square of <#= i #> is <#= i*i #>
   <# } #>
   ```

   ```vb
   <#@ template hostspecific="false" language="VB" #>
   <#@ output extension=".txt" #>
   <#Dim top As Integer = 10

   For i As Integer = 0 To top
   #>
       The square of <#= i #> is <#= i*i #>
   <#
   Next
   #>
   ```

2. Salve o arquivo .tt e inspecione novamente o arquivo .txt gerado. Ele lista os quadrados dos números de 0 a 10.

   Observe que as instruções são incluídas em `<#...#>` e expressões individuais em `<#=...#>`. Para obter mais informações, consulte [escrevendo um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

   Se você escrever o código de geração no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], a diretiva `template` deve conter `language="VB"`. O padrão é `"C#"`.

## <a name="debugging-a-design-time-t4-text-template"></a>Depurando um modelo de texto T4 em tempo de design

Para depurar um modelo de texto:

- Insira `debug="true"` na diretiva `template`. Por exemplo:

   `<#@ template debug="true" hostspecific="false" language="C#" #>`

- Defina pontos de interrupção no modelo, da mesma maneira que você faria para um código comum.

- Escolha **depurar modelo T4** no menu de atalho do arquivo de modelo de texto em Gerenciador de soluções.

   O modelo é executado e é interrompido nos pontos de interrupção. Você pode examinar variáveis ​​e percorrer o código como de costume.

> [!TIP]
> `debug="true"`torna o mapa de código gerado mais precisamente para o modelo de texto, inserindo mais diretivas de numeração de linha no código gerado. Se você deixa-o de fora, os pontos de interrupção podem parar a execução no estado errado.
>
> Mas, você pode deixar a cláusula na diretiva do modelo mesmo quando você não estiver depurando. Isso causa apensa uma pequena queda de desempenho.

## <a name="generating-code-or-resources-for-your-solution"></a>Gerando código ou recursos para sua solução

Você pode gerar arquivos de programas que variam de acordo com o modelo. Um modelo é uma entrada, como um banco de dados, arquivo de configuração, o modelo UML, o modelo DSL ou outra fonte. Geralmente, você gera vários arquivos de programa do mesmo modelo. Para isso, você cria um arquivo de modelo para cada arquivo de programa gerado e faz com que todos os modelos leiam o mesmo modelo.

### <a name="to-generate-program-code-or-resources"></a>Para gerar o código de programa ou recursos

1. Altere a diretiva de saída para gerar um arquivo do tipo apropriado, como .cs, .vb, .resx ou .xml.

2. Insira o código que gerará o código da solução que você precisa. Por exemplo, se você deseja gerar três instruções de campo inteiro em uma classe:

    ```csharp

    <#@ template debug="false" hostspecific="false" language="C#" #>
    <#@ output extension=".cs" #>
    <# var properties = new string [] {"P1", "P2", "P3"}; #>
    // This is generated code:
    class MyGeneratedClass {
    <# // This code runs in the text template:
      foreach (string propertyName in properties)  { #>
      // Generated code:
      private int <#= propertyName #> = 0;
    <# } #>
    }
    ```

    ```vb
    <#@ template debug="false" hostspecific="false" language="VB" #>
    <#@ output extension=".cs" #>
    <# Dim properties = {"P1", "P2", "P3"} #>
    class MyGeneratedClass {
    <#
       For Each propertyName As String In properties
    #>
      private int <#= propertyName #> = 0;
    <#
       Next
    #>
    }

    ```

3. Salve o arquivo e inspecione o arquivo gerado, que agora contém o seguinte código:

    ```csharp
    class MyGeneratedClass {
      private int P1 = 0;
      private int P2 = 0;
      private int P3 = 0;
    }
    ```

### <a name="generating-code-and-generated-text"></a>Gerando código e texto gerado

Quando você gera o código de programa, é muito importante evitar confundir o código de geração que executa em seu modelo e o código gerado resultante que se torna parte de sua solução. As duas linguagens não precisam ser a mesma.

O exemplo anterior tem duas versões. Em uma versão, o código de geração está em C#. Em outra versão, o código de geração está em Visual Basic. Mas o texto gerado por ambos é o mesmo e é uma classe C#.

Da mesma forma, você pode usar um modelo [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] para gerar código em qualquer linguagem. O texto gerado não precisa estar em qualquer linguagem em particular e não tem que ser um código de programa.

### <a name="structuring-text-templates"></a>Estruturando modelos de texto

Por uma questão de práticas recomendadas, nós tendemos a separar o código de modelo em duas partes:

- A parte de configuração ou de coleta de dados, que define os valores das variáveis, mas não contém os blocos de texto. No exemplo anterior, essa parte é a inicialização das `properties`.

   Costumamos chamar isso de seção "modelo", porque ela constrói um modelo no repositório, normalmente, lê um arquivo de modelo.

- A parte de geração de texto (`foreach(...){...}` no exemplo), que usa os valores das variáveis.

   Essa não é a separação necessária, mas é um estilo que torna mais fácil a leitura do modelo, reduzindo a complexidade da parte que inclui o texto.

## <a name="reading-files-or-other-sources"></a>Lendo arquivos ou outras fontes

Para acessar um arquivo de modelo ou banco de dados, o código de modelo pode usar conjuntos como o System.XML. Para ter acesso a esses assemblies, você deve inserir diretivas como estas:

```
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.IO" #>
```

A `assembly` diretiva disponibiliza o assembly especificado para seu código de modelo, da mesma maneira que a seção References de um projeto do Visual Studio. Você não precisa incluir uma referência em System.dll, ele é referenciado automaticamente. A diretiva `import` permite que você use os tipos sem usar seus nomes totalmente qualificados, da mesma forma como a diretiva `using` em um arquivo de programa normal.

Por exemplo, depois de importar **System.Io**, você poderia escrever:

```csharp

<# var properties = File.ReadLines("C:\\propertyList.txt");#>
...
<# foreach (string propertyName in properties) { #>
...
```

```vb
<# For Each propertyName As String In
             File.ReadLines("C:\\propertyList.txt")
#>
```

### <a name="opening-a-file-with-a-relative-pathname"></a>Abrindo um arquivo com um nome de caminho relativo

Para carregar um arquivo de um local referente ao modelo de texto, você pode usar o `this.Host.ResolvePath()`. Para usar este .Host, você deve definir `hostspecific="true"` no `template`:

```
<#@ template debug="false" hostspecific="true" language="C#" #>
```

Depois, você pode escrever, por exemplo:

```csharp
<# string fileName = this.Host.ResolvePath("filename.txt");
  string [] properties = File.ReadLines(filename);
#>
...
<#  foreach (string propertyName in properties { #>
...
```

```vb
<# Dim fileName = Me.Host.ResolvePath("propertyList.txt")
   Dim properties = File.ReadLines(filename)
#>
...
<#   For Each propertyName As String In properties
...
#>
```

Você também pode usar o `this.Host.TemplateFile`, que identifica o nome do arquivo de modelo atual.

O tipo de `this.Host` (no VB, `Me.Host`) é `Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost`.

### <a name="getting-data-from-visual-studio"></a>Obtendo dados do Visual Studio

Para usar os serviços fornecidos no Visual Studio, defina o `hostSpecific` atributo e carregue o `EnvDTE` assembly. Importar `Microsoft.VisualStudio.TextTemplating` , que contém o `GetCOMService()` método de extensão.  Você pode usar ServiceProvider.GetCOMService() para acessar o DTE e outros serviços. Por exemplo:

```src
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetCOMService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

> [!TIP]
> Um modelo de texto é executado em seu próprio domínio de aplicativo e os serviços são acessados ​​por empacotamento. Nesse caso, GetCOMService() é mais confiável que GetService().

## <a name="regenerating-the-code-automatically"></a><a name="Regenerating"></a>Regenerando o código automaticamente

Normalmente, vários arquivos em uma solução do Visual Studio são gerados com um modelo de entrada. Cada arquivo é gerado a partir do seu próprio modelo, mas todos os modelos se referem ao mesmo modelo.

Se o modelo de fonte mudar, você deve executar novamente todos os modelos na solução. Para fazer isso manualmente, escolha **transformar todos os modelos** no menu **Compilar** .

Se você instalou o SDK de modelagem do Visual Studio, você pode ter todos os modelos transformados automaticamente sempre que você executar uma compilação. Para fazer isso, edite o arquivo do projeto (.csproj ou .vbproj) em um editor de texto e adicione as seguintes linhas perto do final do arquivo, depois de qualquer outra instrução `<import>`:

> [!NOTE]
> O SDK de transformação de modelo de texto e o SDK de modelagem do Visual Studio são instalados automaticamente quando você instala recursos específicos do Visual Studio. Para obter mais detalhes, consulte [esta postagem no blog](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/).

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

Para obter mais informações, consulte [geração de código em um processo de compilação](../modeling/code-generation-in-a-build-process.md).

## <a name="error-reporting"></a>Relatório de erros

Para inserir mensagens de erro e aviso na janela de erro do Visual Studio, você pode usar estes métodos:

```
Error("An error message");
Warning("A warning message");
```

## <a name="converting-an-existing-file-to-a-template"></a><a name="Converting"></a>Convertendo um arquivo existente em um modelo

Um recurso útil dos modelos é que eles parecem muito com os arquivos que eles geram, além de um código de programa inserido. Isso sugere um método útil para a criação de um modelo. Primeiro, crie um arquivo comum como um protótipo, como um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] arquivo, e, em seguida, introduza gradualmente o código de geração que varia o arquivo resultante.

### <a name="to-convert-an-existing-file-to-a-design-time-template"></a>Para converter um arquivo existente para um modelo de tempo de design

1. Para o projeto do Visual Studio, adicione um arquivo do tipo que você deseja gerar, como um `.cs` `.vb` arquivo, ou `.resx` .

2. Teste o novo arquivo para conferir se ele funciona.

3. Em Gerenciador de Soluções, altere a extensão de nome de arquivo para **. tt**.

4. Verifique as seguintes propriedades do arquivo **. tt** :

   | | |
   |-|-|
   | **Ferramenta personalizada =** | **TextTemplatingFileGenerator** |
   | **Build Action =** | **Nenhuma** |

5. Insira as seguintes linhas no início do arquivo:

   ```
   <#@ template debug="false" hostspecific="false" language="C#" #>
   <#@ output extension=".cs" #>
   ```

    Se você quiser escrever o código de geração do seu modelo no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], defina o atributo `language` como `"VB"` em vez de `"C#"`.

    Defina o atributo `extension` para a extensão de nome de arquivo para o tipo de arquivo que você deseja gerar, por exemplo `.cs`, `.resx` ou `.xml`.

6. Salve o arquivo.

    Um arquivo subsidiário é criado com a extensão especificada. As propriedades dele estão corretas para o tipo de arquivo. Por exemplo, a propriedade de **ação de compilação** de um arquivo. cs seria **compilada**.

    Verifique se o arquivo gerado contém o mesmo conteúdo que o arquivo original.

7. Identifique uma parte do arquivo que você deseja variar. Por exemplo, uma parte que aparece apenas sob certas condições, uma parte que se repete ou em que os valores específicos variam. Insira o código de geração. Salve o arquivo e verifique se o arquivo subsidiário é gerado corretamente. Repita esta etapa.

## <a name="guidelines-for-code-generation"></a>Diretrizes para a geração de código

Consulte as [diretrizes para escrever modelos de texto T4](../modeling/guidelines-for-writing-t4-text-templates.md).

## <a name="next-steps"></a>Próximas etapas

|Próxima etapa|Tópico|
|-|-|
|Escreva e depure um modelo de texto mais avançado, com código que usa funções auxiliares, arquivos e dados externos incluídos.|[Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)|
|Gere documentos a partir de modelos em tempo de execução.|[Geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md)|
|Execute a geração de texto fora do Visual Studio.|[Gerando arquivos com o utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md)|
|Transforme dados na forma de uma linguagem específica do domínio.|[Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)|
|Grave processadores de diretivas para transformar suas próprias fontes de dados.|[Personalizando transformação de texto T4](../modeling/customizing-t4-text-transformation.md)|

## <a name="see-also"></a>Confira também

- [Diretrizes para escrever modelos de texto T4](../modeling/guidelines-for-writing-t4-text-templates.md)
