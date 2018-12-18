---
title: Geração em um processo de compilação de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
ms.assetid: 4da43429-2a11-4d7e-b2e0-9e4af7033b5a
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: e7cadbf9d4d99fa9deaf4d71545f43d2bf49a3f3
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281804"
---
# <a name="code-generation-in-a-build-process"></a>Geração de código em um processo de build
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Transformação de texto pode ser chamada como parte do processo de compilação de uma solução do Visual Studio. Há tarefas de compilação que são especializadas para a transformação de texto. As tarefas de compilação T4 executam modelos de texto de tempo de design e também compilam modelos de texto de tempo de execução (pré-processados).

Há algumas diferenças em termos do que as tarefas de compilação podem fazer, dependendo do mecanismo de compilação que você usa. Quando você compila a solução no Visual Studio, um modelo de texto pode acessar a API do Visual Studio (EnvDTE) se o [hostspecific = "true"](../modeling/t4-template-directive.md) atributo é definido. Mas isso não ocorre quando você compila a solução a partir da linha de comando ou ao iniciar uma compilação do servidor com o Visual Studio. Nesses casos, a compilação é executada pelo MSBuild e um host T4 diferente é usado.

Isso significa que você não pode acessar itens como nomes de arquivo do projeto da mesma forma quando você cria um modelo de texto no MSBuild. No entanto, você pode [passar informações de ambiente para modelos de texto e processadores de diretriz usando parâmetros de compilação](#parameters).

##  <a name="buildserver"></a> Configurar seus computadores

Para habilitar tarefas de compilação no seu computador de desenvolvimento, instale [SDK de modelagem do Visual Studio](http://www.microsoft.com/download/details.aspx?id=40754).

Se [seu servidor de compilação](http://msdn.microsoft.com/library/788443c3-0547-452e-959c-4805573813a9) é executado em um computador no qual o Visual Studio não estiver instalado, copie os seguintes arquivos para o computador de build do seu computador de desenvolvimento. Substitua os números da versão mais recente por ‘*’.

-   $(ProgramFiles)\MSBuild\Microsoft\VisualStudio\v*.0\TextTemplating

    -   Microsoft.VisualStudio.TextTemplating.Sdk.Host.*.0.dll

    -   Microsoft.TextTemplating.Build.Tasks.dll

    -   Microsoft.TextTemplating.targets

-   $(ProgramFiles)\Microsoft Visual Studio *.0\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

    -   Microsoft.VisualStudio.TextTemplating.*.0.dll

    -   Microsoft.VisualStudio.TextTemplating.Interfaces.*.0.dll (vários arquivos)

    -   Microsoft.VisualStudio.TextTemplating.VSHost.*.0.dll

-   $(ProgramFiles)\Microsoft Visual Studio *.0\Common7\IDE\PublicAssemblies\

    -   Microsoft.VisualStudio.TextTemplating.Modeling.*.0.dll

## <a name="to-edit-the-project-file"></a>Para editar o arquivo do projeto

Você precisará editar o arquivo do projeto para configurar alguns dos recursos no MSBuild.

No Gerenciador de soluções, escolha **Unload** no menu de contexto do seu projeto. Isso permite que você edite o arquivo .csproj ou .vbproj no editor de XML.

Quando tiver terminado a edição, escolha **recarregar**.

## <a name="import-the-text-transformation-targets"></a>Importar os destinos da transformação de texto

No arquivo .vbproj ou .csproj, localize uma linha como esta:

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- ou -

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

Depois dessa linha, insira a importação de modelagem de texto:

```xml
<!-- Optionally make the import portable across VS versions -->
  <PropertyGroup>
    <!-- Get the Visual Studio version – defaults to 10: -->
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">10.0</VisualStudioVersion>
    <!-- Keep the next element all on one line: -->
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
  </PropertyGroup>

<!-- This is the important line: -->
  <Import Project="$(VSToolsPath)\TextTemplating\Microsoft.TextTemplating.targets" />
```

## <a name="transforming-templates-in-a-build"></a>Transformando modelos em uma compilação

Há algumas propriedades que podem ser inseridas em seu arquivo de projeto para controlar a tarefa de transformação:

-   Execute a tarefa Transform no início de cada compilação:

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

-   Substitua os arquivos que são somente leitura, por exemplo, porque eles não passam por check-out:

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

-   Transforme cada modelo toda vez:

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

## <a name="source-control"></a>Controle do código-Fonte

Não há integração interna específica com um sistema de controle do código-fonte. No entanto, você pode adicionar suas próprias extensões, por exemplo, para fazer check-out e check-in de um arquivo gerado. Por padrão, a tarefa de transformação de texto impede que um arquivo seja marcado como somente leitura e, quando esse arquivo é localizado, um erro é registrado na lista de erros do Visual Studio e a tarefa falha.

Para especificar que os arquivos somente leitura devem ser substituídos, insira esta propriedade:

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

A menos que você personalize a etapa de pós-processamento, um aviso será registrado na lista de erros quando um arquivo for substituído.

## <a name="customizing-the-build-process"></a>Personalizando o processo de compilação

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

Especificar OutputFileName ou OutputFilePath não é recomendado se você também estiver transformando modelos no VS usando Transformar Tudo ou executando o gerador de único arquivo. Você acabará com caminhos de arquivos diferentes dependendo de como tiver desencadeado a transformação. Isso pode ser muito confuso.

## <a name="adding-reference-and-include-paths"></a>Adicionando referência e incluir caminhos

O host tem um conjunto padrão de caminhos em que procura assemblies referenciados em modelos. Para adicionar a este conjunto:

```
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

Para definir as pastas em que arquivos de inclusão serão procurados, forneça uma lista separada por ponto-e-vírgula. Normalmente, você adiciona à lista de pastas existente.

```
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

##  <a name="parameters"></a> Passar dados de contexto de build para os modelos

Você pode definir valores de parâmetros no arquivo do projeto. Por exemplo, você pode passar as propriedades de compilação e [variáveis de ambiente](../msbuild/how-to-use-environment-variables-in-a-build.md):

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

##  <a name="msbuild"></a> Usando propriedades do projeto no assembly e diretivas de inclusão

Macros do Visual Studio como $(SolutionDir) não funcionam no MSBuild. Você pode usar as propriedades do projeto como alternativa.

Edite seu arquivo .csproj ou .vbproj para definir uma propriedade do projeto. Este exemplo define uma propriedade chamada `myLibFolder`:

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

Se você atualizar um arquivo incluído ou outro arquivo lido pelo modelo, o Visual Studio não transformará o arquivo automaticamente. Transformar modelos como parte da compilação assegura que tudo seja atualizado.

**O que outras opções existem para transformar modelos de texto?**

-   O [utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md) podem ser usados em scripts de comando. Na maioria dos casos, é mais fácil usar o MSBuild.

-   [Invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md)

-   [Modelos de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md) são transformados pelo Visual Studio.

-   [Modelos de texto de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md) são transformados em tempo de execução em seu aplicativo.

## <a name="read-more"></a>Leia mais

Há uma boa orientação no modelo T4 do MSbuild, $(VSToolsPath)\TextTemplating\Microsoft.TextTemplating.targets

- [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
- [Visualização do Visual Studio e SDK de modelagem](http://go.microsoft.com/fwlink/?LinkID=185579)
- [{1&gt;{2&gt;oleg Sych: Noções básicas sobre a integração de T4:MSBuild](http://www.olegsych.com/2010/04/understanding-t4-msbuild-integration/)