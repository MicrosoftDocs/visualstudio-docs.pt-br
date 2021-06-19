---
title: Geração de código em um processo de compilação
description: Saiba como a transformação de texto pode ser invocada como parte do processo de build de uma Visual Studio de texto.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7db1b41df5007678c84be71f34aea110c04348c1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389742"
---
# <a name="invoke-text-transformation-in-the-build-process"></a>Invocar transformação de texto no processo de build

[A transformação](../modeling/code-generation-and-t4-text-templates.md) de texto pode ser invocada como parte do processo [de build](/azure/devops/pipelines/index) de uma Visual Studio solução. Há tarefas de compilação que são especializadas para a transformação de texto. As tarefas de compilação T4 executam modelos de texto de tempo de design e também compilam modelos de texto de tempo de execução (pré-processados).

Há algumas diferenças em termos do que as tarefas de compilação podem fazer, dependendo do mecanismo de compilação que você usa. Quando você cria a solução no Visual Studio, um modelo de texto pode acessar a API Visual Studio (EnvDTE) se o [atributo hostspecific="true"](../modeling/t4-template-directive.md) estiver definido. Mas isso não é verdadeiro quando você cria a solução na linha de comando ou quando inicia um build de servidor por meio de Visual Studio. Nesses casos, a compilação é executada pelo MSBuild e um host T4 diferente é usado. Isso significa que você não pode acessar coisas como nomes de arquivo de projeto da mesma maneira ao criar um modelo de texto usando o MSBuild. No entanto, você pode [passar informações de ambiente para modelos de texto e processadores de](#parameters)diretiva usando parâmetros de build .

## <a name="configure-your-machines"></a><a name="buildserver"></a> Configurar seus máquinas

Para habilitar tarefas de build em seu computador de desenvolvimento, instale o SDK de Modelagem para Visual Studio.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Se [o servidor de build](/azure/devops/pipelines/agents/agents) for executado em um computador que não Visual Studio instalado, copie os seguintes arquivos para o computador de build do computador de desenvolvimento:

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\MSBuild\Microsoft\VisualStudio\v16.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.15.0.dll
  - Microsoft.TextTemplating.Build.Tasks.dll
  - Microsoft.TextTemplating.targets

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.Interfaces.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.VSHost.15.0.dll

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\IDE\PublicAssemblies

  - Microsoft.VisualStudio.TextTemplating.Modeling.15.0.dll

> [!TIP]
> Se você obter um para um método Microsoft.CodeAnalysis ao executar destinos de build TextTemplating em um servidor de build, certifique-se de que os assemblies roslyn estão em um diretório chamado Roslyn que está no mesmo diretório que o executável de build `MissingMethodException` (por exemplo, *msbuild.exe*). 

## <a name="edit-the-project-file"></a>Editar o arquivo de projeto

Edite o arquivo de projeto para configurar alguns dos recursos no MSBuild, por exemplo, importando os destinos de transformação de texto.

No **Gerenciador de Soluções**, escolha **Descarregar** no menu de clique com o botão direito do mouse do projeto. Isso permite que você edite o arquivo .csproj ou .vbproj no editor de XML. Quando terminar de editar, escolha **Recarregar**.

## <a name="import-the-text-transformation-targets"></a>Importar os destinos de transformação de texto

No arquivo .vbproj ou .csproj, localize uma linha como esta:

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- ou –

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

Depois dessa linha, insira a importação de modelagem de texto:

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

## <a name="transform-templates-in-a-build"></a>Transformar modelos em um build

Há algumas propriedades que podem ser inseridas em seu arquivo de projeto para controlar a tarefa de transformação:

- Execute a tarefa Transform no início de cada compilação:

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- Substituir arquivos que são somente leitura, por exemplo, porque eles não são verificados:

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

     Por padrão, a tarefa T4 MSBuild regenera um arquivo de saída se for mais antigo do que:

     - seu arquivo de modelo
     - todos os arquivos incluídos
     - todos os arquivos que foram lidos anteriormente pelo modelo ou por um processador de diretiva que ele usa

     Esse é um teste de dependência mais poderoso do que é usado pelo comando **Transformar** Todos os Modelos no Visual Studio, que compara apenas as datas do modelo e do arquivo de saída.

Para executar apenas as transformações de texto em seu projeto, invoque a tarefa TransformAll:

`msbuild myProject.csproj /t:TransformAll`

Para transformar um modelo específico de texto:

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

Você pode usar curingas em TransformFile:

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>Controle do código-fonte

Não há integração interna específica com um sistema de controle do código-fonte. No entanto, você pode adicionar suas próprias extensões, por exemplo, para fazer check-out e fazer check-in de um arquivo gerado. Por padrão, a tarefa de transformação de texto evita a substituição de um arquivo marcado como somente leitura. Quando esse arquivo é encontrado, um erro é registrado na lista Visual Studio erros e a tarefa falha.

Para especificar que os arquivos somente leitura devem ser substituídos, insira esta propriedade:

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

A menos que você personalize a etapa de pós-processamento, um aviso será registrado na Lista de Erros quando um arquivo for substituído.

## <a name="customize-the-build-process"></a>Personalizar o processo de build

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

- GeneratedFiles – uma lista de arquivos gravados pelo processo. Para os arquivos que sobrescreviam arquivos somente leitura existentes, `%(GeneratedFiles.ReadOnlyFileOverwritten)` será true. Esses arquivos podem passar por check-out do controle do código-fonte.

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

Uma pasta útil para redirecionar é `$(IntermediateOutputPath)` .

Se você especificar um nome de arquivo de saída, ele tem precedência sobre a extensão especificada na diretiva de saída nos modelos.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

Especificar um OutputFileName ou OutputFilePath não será recomendado se você também estiver transformando modelos dentro Visual Studio usando Transformar **Tudo** ou executando o gerador de arquivo único. Você acabará com caminhos de arquivo diferentes dependendo de como você disparou a transformação. Isso pode ser confuso.

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

## <a name="pass-build-context-data-into-the-templates"></a><a name="parameters"></a> Passar dados de contexto de build para os modelos

Você pode definir valores de parâmetros no arquivo do projeto. Por exemplo, você pode passar propriedades [de build](../msbuild/msbuild-properties.md) e [variáveis de ambiente](../msbuild/how-to-use-environment-variables-in-a-build.md):

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

Em um modelo de texto, defina `hostspecific` na diretiva do modelo. Use a [diretiva parameter](../modeling/t4-parameter-directive.md) para obter valores:

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

Em um processador de diretiva, você pode chamar [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)):

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> `ResolveParameterValue` obtém dados `T4ParameterValues` somente quando você usa o MSBuild. Quando você transforma o modelo usando Visual Studio, os parâmetros têm valores padrão.

## <a name="use-project-properties-in-assembly-and-include-directives"></a><a name="msbuild"></a> Usar propriedades do projeto no assembly e incluir diretivas

Visual Studio macros como **$(SolutionDir)** não funcionam no MSBuild. Você pode usar as propriedades do projeto como alternativa.

Edite *o arquivo .csproj* *ou .vbproj* para definir uma propriedade de projeto. Este exemplo define uma propriedade chamada **myLibFolder**:

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

## <a name="q--a"></a>Perguntas e Respostas

**Por que eu gostaria de transformar modelos no servidor de build? Já transformei modelos em Visual Studio antes de verificar meu código.**

Se você atualizar um arquivo incluído ou outro arquivo lido pelo modelo, o Visual Studio não transformará o arquivo automaticamente. Transformar modelos como parte do build garante que tudo está atualizado.

**Quais são as outras opções disponíveis para transformar modelos de texto?**

- O [utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md) pode ser usado em scripts de comando. Na maioria dos casos, é mais fácil usar o MSBuild.

- [Invocar a transformação de texto em uma extensão do Visual Studio](../modeling/invoking-text-transformation-in-a-vs-extension.md).

- [Modelos de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md) são transformados pelo Visual Studio.

- Os [modelos de texto de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md) são transformados em tempo de execução em seu aplicativo.

## <a name="see-also"></a>Confira também

::: moniker range="vs-2017"

- Há uma boa orientação no modelo de MSbuild do T4 em `%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

::: moniker range=">=vs-2019"

- Há uma boa orientação no modelo de MSbuild do T4 em `%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\msbuild\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

- [Escrever um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
