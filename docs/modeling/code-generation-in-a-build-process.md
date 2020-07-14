---
title: Geração de código em um processo de compilação
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 1fd7538782bff80ee12ac0aa0e66c0daa4da2d5c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546712"
---
# <a name="invoke-text-transformation-in-the-build-process"></a>Invocar a transformação de texto no processo de compilação

A [transformação de texto](../modeling/code-generation-and-t4-text-templates.md) pode ser chamada como parte do processo de [compilação](/azure/devops/pipelines/index) de uma solução do Visual Studio. Há tarefas de compilação que são especializadas para a transformação de texto. As tarefas de compilação T4 executam modelos de texto de tempo de design e também compilam modelos de texto de tempo de execução (pré-processados).

Há algumas diferenças em termos do que as tarefas de compilação podem fazer, dependendo do mecanismo de compilação que você usa. Quando você cria a solução no Visual Studio, um modelo de texto pode acessar a API do Visual Studio (EnvDTE) se o atributo [hostspecific = "true"](../modeling/t4-template-directive.md) estiver definido. Mas isso não é verdadeiro quando você cria a solução na linha de comando ou quando inicia uma compilação de servidor por meio do Visual Studio. Nesses casos, a compilação é executada pelo MSBuild e um host T4 diferente é usado. Isso significa que você não pode acessar itens como nomes de arquivo de projeto da mesma maneira quando cria um modelo de texto usando o MSBuild. No entanto, você pode [passar informações de ambiente em modelos de texto e processadores de diretiva usando parâmetros de compilação](#parameters).

## <a name="configure-your-machines"></a><a name="buildserver"></a>Configurar seus computadores

Para habilitar tarefas de compilação em seu computador de desenvolvimento, instale o SDK de modelagem para Visual Studio.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Se [o servidor de compilação](/azure/devops/pipelines/agents/agents) for executado em um computador que não tem o Visual Studio instalado, copie os seguintes arquivos para o computador de compilação do computador de desenvolvimento:

- % ProgramFiles (x86)% \ Microsoft Visual Studio\2019\Community\MSBuild\Microsoft\VisualStudio\v16.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.15.0.dll
  - Microsoft.TextTemplating.Build.Tasks.dll
  - Microsoft.TextTemplating.targets

- % ProgramFiles (x86)% \ Microsoft Visual Studio\2019\Community\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.Interfaces.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.VSHost.15.0.dll

- % ProgramFiles (x86)% \ Microsoft Visual Studio\2019\Community\Common7\IDE\PublicAssemblies

  - Microsoft.VisualStudio.TextTemplating.Modeling.15.0.dll

> [!TIP]
> Se você receber um `MissingMethodException` para um método Microsoft. CodeAnalysis ao executar destinos de compilação TextTemplating em um servidor de compilação, verifique se os assemblies Roslyn estão em um diretório chamado *Roslyn* que está no mesmo diretório que o executável de compilação (por exemplo, *msbuild.exe*).

## <a name="edit-the-project-file"></a>Editar o arquivo de projeto

Edite o arquivo de projeto para configurar alguns dos recursos no MSBuild, por exemplo, importando os destinos de transformação de texto.

Em **Gerenciador de soluções**, escolha **descarregar** no menu de atalho do seu projeto. Isso permite que você edite o arquivo .csproj ou .vbproj no editor de XML. Quando terminar de editar, escolha **recarregar**.

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

## <a name="transform-templates-in-a-build"></a>Transformar modelos em uma compilação

Há algumas propriedades que podem ser inseridas em seu arquivo de projeto para controlar a tarefa de transformação:

- Execute a tarefa Transform no início de cada compilação:

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- Substituir arquivos que são somente leitura, por exemplo, porque eles não têm check-out:

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

     Por padrão, a tarefa T4 MSBuild regenera um arquivo de saída se ele for mais antigo que:

     - seu arquivo de modelo
     - todos os arquivos incluídos
     - todos os arquivos que foram lidos anteriormente pelo modelo ou por um processador de diretiva que ele usa

     Esse é um teste de dependência mais potente do que é usado pelo comando **transformar todos os modelos** no Visual Studio, que só compara as datas do modelo e do arquivo de saída.

Para executar apenas as transformações de texto em seu projeto, invoque a tarefa TransformAll:

`msbuild myProject.csproj /t:TransformAll`

Para transformar um modelo específico de texto:

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

Você pode usar curingas em TransformFile:

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>Controle do código-fonte

Não há integração interna específica com um sistema de controle do código-fonte. No entanto, você pode adicionar suas próprias extensões, por exemplo, para fazer check-out e fazer check-in de um arquivo gerado. Por padrão, a tarefa de transformação de texto evita a substituição de um arquivo que está marcado como somente leitura. Quando esse arquivo é encontrado, um erro é registrado no Lista de Erros do Visual Studio e a tarefa falha.

Para especificar que os arquivos somente leitura devem ser substituídos, insira esta propriedade:

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

A menos que você personalize a etapa de pré-processamento, um aviso será registrado no Lista de Erros quando um arquivo for substituído.

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

- GeneratedFiles – uma lista de arquivos gravados pelo processo. Para os arquivos que substituiram os arquivos somente leitura existentes, `%(GeneratedFiles.ReadOnlyFileOverwritten)` serão verdadeiros. Esses arquivos podem passar por check-out do controle do código-fonte.

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

Uma pasta útil para a qual redirecionar é `$(IntermediateOutputPath)` .

Se você especificar um nome de arquivo de saída, ele terá precedência sobre a extensão especificada na diretiva de saída nos modelos.

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

A especificação de um NomeDoArquivoDeSaída ou OutputFilePath não é recomendada se você também estiver transformando modelos dentro do Visual Studio usando **transformar tudo** ou executar o gerador de arquivo único. Você acabará com caminhos de arquivo diferentes, dependendo de como você disparou a transformação. Isso pode ser confuso.

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

## <a name="pass-build-context-data-into-the-templates"></a><a name="parameters"></a>Passar dados de contexto de compilação para os modelos

Você pode definir valores de parâmetros no arquivo do projeto. Por exemplo, você pode passar Propriedades de [compilação](../msbuild/msbuild-properties.md) e [variáveis de ambiente](../msbuild/how-to-use-environment-variables-in-a-build.md):

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

Em um modelo de texto, defina `hostspecific` na diretiva do modelo. Use a diretiva de [parâmetro](../modeling/t4-parameter-directive.md) para obter valores:

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

Em um processador de diretiva, você pode chamar [ITextTemplatingEngineHost. ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\)):

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> `ResolveParameterValue`Obtém dados `T4ParameterValues` somente de quando você usa o MSBuild. Quando você transforma o modelo usando o Visual Studio, os parâmetros têm valores padrão.

## <a name="use-project-properties-in-assembly-and-include-directives"></a><a name="msbuild"></a>Usar as propriedades do projeto no assembly e incluir diretivas

Macros do Visual Studio como **$ (SolutionDir)** não funcionam no MSBuild. Você pode usar as propriedades do projeto como alternativa.

Edite seu arquivo *. csproj* ou *. vbproj* para definir uma propriedade de projeto. Este exemplo define uma propriedade chamada **myLibFolder**:

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

**Por que desejo transformar modelos no servidor de compilação? Já transformamos modelos no Visual Studio antes de fazer check-in do meu código.**

Se você atualizar um arquivo incluído ou outro arquivo lido pelo modelo, o Visual Studio não transforma o arquivo automaticamente. A transformação de modelos como parte da compilação garante que tudo esteja atualizado.

**Quais são as outras opções disponíveis para transformar modelos de texto?**

- O [utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md) pode ser usado em scripts de comando. Na maioria dos casos, é mais fácil usar o MSBuild.

- [Invocar a transformação de texto em uma extensão do Visual Studio](../modeling/invoking-text-transformation-in-a-vs-extension.md).

- [Modelos de texto de tempo de design](../modeling/design-time-code-generation-by-using-t4-text-templates.md) são transformados pelo Visual Studio.

- Os [modelos de texto de tempo de execução](../modeling/run-time-text-generation-with-t4-text-templates.md) são transformados em tempo de execução em seu aplicativo.

## <a name="see-also"></a>Confira também

::: moniker range="vs-2017"

- Há uma boa orientação no modelo de MSbuild do T4 em`%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

::: moniker range=">=vs-2019"

- Há uma boa orientação no modelo de MSbuild do T4 em`%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\msbuild\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

- [Escrever um modelo de texto T4](../modeling/writing-a-t4-text-template.md)
