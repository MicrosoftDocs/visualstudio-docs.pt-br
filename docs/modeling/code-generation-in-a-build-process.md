---
title: Geração de código em um processo de build
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: ef7c49c514c9104ee4659db983b04c27036df889
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281817"
---
# <a name="code-generation-in-a-build-process"></a>Geração de código em um processo de compilação

[Transformação de texto](../modeling/code-generation-and-t4-text-templates.md) pode ser invocado como parte do [processo de compilação](/azure/devops/pipelines/index) de uma solução do Visual Studio. Há tarefas de compilação que são especializadas para a transformação de texto. As tarefas de compilação T4 executam modelos de texto de tempo de design e também compilam modelos de texto de tempo de execução (pré-processados).

Há algumas diferenças em termos do que as tarefas de compilação podem fazer, dependendo do mecanismo de compilação que você usa. Quando você compila a solução no Visual Studio, um modelo de texto pode acessar a API do Visual Studio (EnvDTE) se o [hostspecific = "true"](../modeling/t4-template-directive.md) atributo é definido. Mas isso não é verdadeiro quando você compila a solução da linha de comando ou ao iniciar uma compilação do servidor por meio do Visual Studio. Nesses casos, a compilação é executada pelo MSBuild e um host T4 diferente é usado.

Isso significa que você não pode acessar itens como nomes de arquivo de projeto da mesma forma quando você cria um modelo de texto no MSBuild. No entanto, você pode [passar informações de ambiente para modelos de texto e processadores de diretriz usando parâmetros de compilação](#parameters).

##  <a name="buildserver"></a> Configurar seus computadores

Para habilitar tarefas de compilação no seu computador de desenvolvimento, instale o SDK de modelagem para Visual Studio.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Se [seu servidor de compilação](/azure/devops/pipelines/agents/agents) é executado em um computador no qual o Visual Studio não estiver instalado, copie os seguintes arquivos para o computador de build do seu computador de desenvolvimento. Substitua os números de versão mais recentes para ' *'.

- $(ProgramFiles)\MSBuild\Microsoft\VisualStudio\v*.0\TextTemplating

    - Microsoft.VisualStudio.TextTemplating.Sdk.Host.*.0.dll

    - Microsoft.TextTemplating.Build.Tasks.dll

    - Microsoft.TextTemplating.targets

- $(ProgramFiles)\Microsoft Visual Studio *.0\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

    - Microsoft.VisualStudio.TextTemplating.*.0.dll

    - Microsoft.VisualStudio.TextTemplating.Interfaces.*.0.dll (vários arquivos)

    - Microsoft.VisualStudio.TextTemplating.VSHost.*.0.dll

- $(ProgramFiles)\Microsoft Visual Studio *.0\Common7\IDE\PublicAssemblies\

    - Microsoft.VisualStudio.TextTemplating.Modeling.*.0.dll

## <a name="to-edit-the-project-file"></a>Para editar o arquivo do projeto

Você precisará editar o arquivo de projeto para configurar alguns dos recursos no MSBuild.

Na **Gerenciador de soluções**, escolha **Unload** no menu de contexto do seu projeto. Isso permite que você edite o arquivo .csproj ou .vbproj no editor de XML.

Quando tiver terminado a edição, escolha **recarregar**.

## <a name="import-the-text-transformation-targets"></a>Importar os destinos de transformação de texto

No arquivo .vbproj ou .csproj, localize uma linha como esta:

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- ou -

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

Depois dessa linha, insira a importação de modelagem de texto:

```xml
<!-- Optionally make the import portable across VS versions -->
  <PropertyGroup>
    <!-- Get the Visual Studio version - defaults to 10: -->
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">10.0</VisualStudioVersion>
    <!-- Keep the next element all on one line: -->
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
  </PropertyGroup>

<!-- This is the important line: -->
  <Import Project="$(VSToolsPath)\TextTemplating\Microsoft.TextTemplating.targets" />
```

## <a name="transform-templates-in-a-build"></a>Transformar modelos em uma compilação

Há algumas propriedades que podem ser inseridas em seu arquivo de projeto para controlar a tarefa de transformação:

- Execute a tarefa Transform no início de cada compilação:

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- Substitua os arquivos que são somente leitura, por exemplo, porque eles não passam por check-out:

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

- Transforme cada modelo toda vez:

    ```xml
    <PropertyGroup>
        <TransformOutOfDateOnly>false</TransformOutOfDateOnly>
    </PropertyGroup>
    ```

     Por padrão, a tarefa T4 do MSBuild gera um arquivo de saída se for mais antigo que seu arquivo de modelo, ou que qualquer arquivo incluído ou lido anteriormente pelo modelo ou por um processador de diretriz que ele use. Observe que esse é um teste de dependência muito mais avançado do que é usado pelo comando Transformar Todos os Modelos no Visual Studio, que compara apenas as datas do modelo e do arquivo de saída.

Para executar apenas as transformações de texto em seu projeto, invoque a tarefa TransformAll:

`msbuild myProject.csproj /t:TransformAll`

Para transformar um modelo específico de texto:

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

Você pode usar curingas em TransformFile:

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>Controle do código-fonte

Não há integração interna específica com um sistema de controle do código-fonte. No entanto, você pode adicionar suas próprias extensões, por exemplo, para fazer check-out e check-in de um arquivo gerado. Por padrão, a tarefa de transformação de texto impede que um arquivo seja marcado como somente leitura e, quando esse arquivo é localizado, um erro é registrado na lista de erros do Visual Studio e a tarefa falha.

Para especificar que os arquivos somente leitura devem ser substituídos, insira esta propriedade:

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

A menos que você personalize a etapa de pós-processamento, um aviso será registrado na lista de erros quando um arquivo for substituído.

## <a name="customize-the-build-process"></a>Personalizar o processo de compilação

A transformação de texto ocorre antes de outras tarefas no processo de compilação. Você pode definir as tarefas que são invocadas antes e depois da transformação, definindo as propriedades `$(BeforeTransform)` e `$(AfterTransform)`:

```xml
<PropertyGroup>
    <BeforeTransform>CustomPreTransform</BeforeTransform>
    <AfterTransform>CustomPostTransform</AfterTransform>
  </PropertyGroup>
  <Target Name="CustomPreTransform">
    <Message Text="In CustomPreTransform..." Importance="High" />
  </Target>
  <Target Name="CustomPostTransform">
    <Message Text="In CustomPostTransform..." Importance="High" />
  </Target>
```

Em `AfterTransform`, você pode referenciar listas de arquivos:

- GeneratedFiles – uma lista de arquivos gravados pelo processo. Para os arquivos que substituíram os arquivos somente leitura existentes, %(GeneratedFiles.ReadOnlyFileOverwritten) será true. Esses arquivos podem passar por check-out do controle do código-fonte.

- NonGeneratedFiles – uma lista de arquivos somente leitura que não foram substituídos.

Por exemplo, você definirá uma tarefa fazer check-out de GeneratedFiles.

## <a name="outputfilepath-and-outputfilename"></a>OutputFilePath e OutputFileName

Essas propriedades são usadas somente pelo MSBuild. Elas não afetam a geração de código no Visual Studio. Elas redirecionam o arquivo de saída gerado para uma pasta ou um arquivo diferente. A pasta de destino já deve existir.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFilePath>MyFolder</OutputFilePath>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Uma pasta útil para redirecionar é `$(IntermediateOutputPath).`

Se você especificar o nome do arquivo de saída, ele terá precedência sobre a extensão especificada na diretiva de saída nos modelos.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Especificar OutputFileName ou OutputFilePath não é recomendado se você também estiver transformando modelos no VS usando transformar tudo ou executando o gerador de arquivo único. Você acabará com caminhos de arquivos diferentes dependendo de como tiver desencadeado a transformação. Isso pode ser muito confuso.

## <a name="add-reference-and-include-paths"></a>Adicionar referência e incluir caminhos

O host tem um conjunto padrão de caminhos em que procura assemblies referenciados em modelos. Para adicionar a este conjunto:

```xml
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

Para definir as pastas em que arquivos de inclusão serão procurados, forneça uma lista separada por ponto-e-vírgula. Normalmente, você adiciona à lista de pastas existente.

```xml
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

##  <a name="parameters"></a> Passar dados de contexto de build para os modelos

Você pode definir valores de parâmetros no arquivo do projeto. Por exemplo, você pode passar [construir](../msbuild/msbuild-properties.md) propriedades e [variáveis de ambiente](../msbuild/how-to-use-environment-variables-in-a-build.md):

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

Em um modelo de texto, defina `hostspecific` na diretiva do modelo. Use o [parâmetro](../modeling/t4-parameter-directive.md) diretiva para obter valores:

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

Em um processador de diretriz, você pode chamar [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)):

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> `ResolveParameterValue` obtém dados de `T4ParameterValues` somente quando você usa o MSBuild. Quando você transformar o modelo usando o Visual Studio, os parâmetros terão valores padrão.

##  <a name="msbuild"></a> Use as propriedades do projeto no assembly e diretivas de inclusão

Macros do Visual Studio, como **$ (solutiondir)** não funcionam no MSBuild. Você pode usar as propriedades do projeto como alternativa.

Editar seu *. csproj* ou *. vbproj* arquivo para definir uma propriedade de projeto. Este exemplo define uma propriedade chamada **myLibFolder**:

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

Agora você pode usar sua propriedade de projeto no assembly e diretivas de inclusão:

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
<#@ include file="$(myLibFolder)\MyIncludeFile.t4" #>
```

Essas diretivas obtêm valores de T4parameterValues nos hosts do MSBuild e do Visual Studio.

## <a name="q--a"></a>Perguntas e respostas

**Por que eu quiser transformar modelos no servidor de compilação? Eu já transformei modelos no Visual Studio antes de fazer check-in do meu código.**

Se você atualizar um arquivo incluído ou outro arquivo lido pelo modelo, o Visual Studio não transformará o arquivo automaticamente. Transformando modelos como parte da compilação assegura que tudo está atualizado.

**O que outras opções existem para transformar modelos de texto?**

- O [utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md) podem ser usados em scripts de comando. Na maioria dos casos, é mais fácil de usar o MSBuild.

- [Invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md)

- [Modelos de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md) são transformados pelo Visual Studio.

- [Modelos de texto de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md) são transformados em tempo de execução em seu aplicativo.

## <a name="see-also"></a>Consulte também

- Há boas diretrizes no modelo T4 do MSbuild no *% ProgramFiles (x86) %\Microsoft Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets Visual*
- [Escrever um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
