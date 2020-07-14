---
title: Tarefas embutidas do MSBuild com RoslynCodeTaskFactory | Microsoft Docs
ms.date: 09/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: e72e6506-4a11-4edf-ae8d-cfb5a3b9d8a0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a1f606ed9e3d42d9f57cb941ee9518c1abfbc47
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289203"
---
# <a name="msbuild-inline-tasks-with-roslyncodetaskfactory"></a>Tarefas embutidas do MSBuild com RoslynCodeTaskFactory

Semelhante ao [CodeTaskFactory](../msbuild/msbuild-inline-tasks.md), o RoslynCodeTaskFactory usa os compiladores Roslyn multiplataforma para gerar assemblies de tarefa na memória a serem usados como tarefas embutidas.  As tarefas do RoslynCodeTaskFactory são direcionadas ao .NET Standard e podem trabalhar nos runtimes do .NET Framework e do .NET Core, bem como no de outras plataformas, como Linux e Mac OS.

>[!NOTE]
>O RoslynCodeTaskFactory está disponível apenas no MSBuild 15.8 e superiores. As versões do MSBuild seguem versões do Visual Studio, portanto, o RoslynCodeTaskFactory está disponível no Visual Studio 2017 versão 15,8 e superior.

## <a name="the-structure-of-an-inline-task-with-roslyncodetaskfactory"></a>A estrutura de uma tarefa embutida com RoslynCodeTaskFactory

 As tarefas embutidas do RoslynCodeTaskFactory são declaradas de forma idêntica às do [CodeTaskFactory](../msbuild/msbuild-inline-tasks.md), a única diferença é que elas são direcionadas ao .NET Standard.  Normalmente, a tarefa embutida e o elemento `UsingTask` que a contém são incluídos em um arquivo *.targets* e importados para outros arquivos de projeto conforme a necessidade. Veja uma tarefa básica em linha. Observe que ela não faz nada.

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task does nothing. -->
  <UsingTask
    TaskName="DoNothing"
    TaskFactory="RoslynCodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="" />
      <Using Namespace="" />
      <Code Type="Fragment" Language="cs">
      </Code>
    </Task>
  </UsingTask>
</Project>
```

 O elemento `UsingTask` no exemplo tem três atributos que descrevem a tarefa e a fábrica de tarefas em linha que a compila.

- O atributo `TaskName` nomeia a tarefa, neste caso, `DoNothing`.

- O atributo `TaskFactory` nomeia a classe que implementa a fábrica de tarefas em linha.

- O atributo `AssemblyFile` fornece o local da fábrica de tarefas em linha. Como alternativa, você pode usar o atributo `AssemblyName` para especificar o nome totalmente qualificado da classe de fábrica de tarefas em linha, que normalmente está localizado no GAC (cache de assembly global).

Os elementos restantes da tarefa `DoNothing` estão vazios w são fornecidos para ilustrar a ordem e a estrutura de uma tarefa em linha. Um exemplo mais robusto será apresentado posteriormente neste tópico.

- O elemento `ParameterGroup` é opcional. Quando especificado, ele declara os parâmetros para a tarefa. Para obter mais informações sobre os parâmetros de entrada e saída, consulte [parâmetros de entrada e saída](#input-and-output-parameters) mais adiante neste tópico.

- O elemento `Task` descreve e contém o código de origem da tarefa.

- O elemento `Reference` especifica referências aos assemblies do .NET que você está usando em seu código. Isso equivale à adição de uma referência a um projeto no Visual Studio. O atributo `Include` especifica o caminho do assembly referenciado.

- O elemento `Using` lista os namespaces que você deseja acessar. Isso se assemelha à instrução `Using` no Visual C#. O atributo `Namespace` especifica o namespace a ser incluído.

Os elementos `Reference`e `Using` independem da linguagem. As tarefas em linha podem ser escritas em qualquer idioma com suporte do CodeDom .NET, por exemplo, Visual Basic ou Visual C#.

> [!NOTE]
> Os elementos contidos pelo elemento `Task` são específicos da fábrica de tarefas, nesse caso, a fábrica de tarefas de código.

### <a name="code-element"></a>Elemento de código

O último elemento filho a aparecer no elemento `Task` é o elemento `Code`. O elemento `Code` contém ou localiza o código que você deseja compilar em uma tarefa. O que é colocado no elemento `Code` depende de como você deseja escrever a tarefa.

O atributo `Language` especifica a linguagem em que seu código é escrito. Os valores aceitáveis são `cs` para C#, `vb` para Visual Basic.

O atributo `Type` especifica o tipo de código que é encontrado no elemento `Code`.

- Se o valor de `Type` é `Class`, o elemento `Code` contém o código para uma classe que deriva da interface <xref:Microsoft.Build.Framework.ITask>.

- Se o valor de `Type` é `Method`, o código define uma substituição do método `Execute` da interface <xref:Microsoft.Build.Framework.ITask>.

- Se o valor de `Type` é `Fragment`, o código define o conteúdo do método `Execute`, mas não a assinatura ou a instrução `return`.

O próprio código normalmente aparece entre um marcador `<![CDATA[` e um marcador `]]>`. Como o código está em uma seção CDATA, você não precisa se preocupar com a saída de caracteres reservados, por exemplo, " \<" or "> ".

Como alternativa, você pode usar o atributo `Source` do elemento `Code` para especificar o local de um arquivo que contém o código da sua tarefa. O código no arquivo de origem deve ser do tipo especificado pelo atributo `Type`. Se o atributo `Source` estiver presente, o valor padrão de `Type` será `Class`. Se `Source` é não estiver presente, o valor padrão será `Fragment`.

> [!NOTE]
> Ao definir a classe de tarefa no arquivo de origem, o nome da classe deve concordar com o atributo `TaskName` do elemento [UsingTask](../msbuild/usingtask-element-msbuild.md) correspondente.

## <a name="hello-world"></a>Olá, Mundo

 Aqui está uma tarefa embutida mais robusta com RoslynCodeTaskFactory. A tarefa HelloWorld exibe "Hello, world!" no dispositivo de registro de erros em log padrão, que é normalmente o console do sistema ou a janela **Saída** do Visual Studio. O elemento `Reference` no exemplo é incluído apenas para ilustração.

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task displays "Hello, world!" -->
  <UsingTask
    TaskName="HelloWorld"
    TaskFactory="RoslynCodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="System.Xml"/>
      <Using Namespace="System"/>
      <Using Namespace="System.IO"/>
      <Code Type="Fragment" Language="cs">
<![CDATA[
// Display "Hello, world!"
Log.LogError("Hello, world!");
]]>
      </Code>
    </Task>
  </UsingTask>
</Project>
```

Salve a tarefa HelloWorld em um arquivo chamado *HelloWorld.targets* e, em seguida, invoque-o em um projeto conforme mostrado a seguir.

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="HelloWorld.targets" />
  <Target Name="Hello">
    <HelloWorld />
  </Target>
</Project>
```

## <a name="input-and-output-parameters"></a>Parâmetros de entrada e de saída

 Os parâmetros de tarefa em linha são elementos filhos de um elemento `ParameterGroup`. Cada parâmetro tem o nome do elemento que o define. O código a seguir define o parâmetro `Text`.

```xml
<ParameterGroup>
    <Text />
</ParameterGroup>
```

Os parâmetros podem ter um ou mais destes atributos:

- `Required` é um atributo opcional que é `false` por padrão. Se `true`, o parâmetro é necessário e deve receber um valor antes de chamar a tarefa.

- `ParameterType` é um atributo opcional que é `System.String` por padrão. Ele pode ser definido como qualquer tipo totalmente qualificado que seja um item ou um valor que pode ser convertido em uma cadeia de caracteres usando System.Convert.ChangeType. (Em outras palavras, qualquer tipo que possa ser passado de e para uma tarefa externa.)

- `Output` é um atributo opcional que é `false` por padrão. Se `true`, o parâmetro deve receber um valor antes de retornar do método Execute.

Por exemplo,

```xml
<ParameterGroup>
    <Expression Required="true" />
    <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
    <Tally ParameterType="System.Int32" Output="true" />
</ParameterGroup>
```

define esses três parâmetros:

- `Expression` é um parâmetro de entrada obrigatório do tipo System.String.

- `Files` é um parâmetro de entrada de lista do item obrigatório.

- `Tally`é um parâmetro de saída do tipo System.Int32.

Se o elemento `Code` tem o atributo `Type` de `Fragment` ou `Method`, as propriedades são criadas automaticamente para cada parâmetro.  Em RoslynCodeTaskFactory, se o `Code` elemento tiver o `Type` atributo de `Class` , você não precisará especificar o `ParameterGroup` , pois ele é inferido do código-fonte (essa é uma diferença de `CodeTaskFactory` ). Caso contrário, as propriedades devem ser declaradas explicitamente no código-fonte da tarefa e devem coincidir exatamente com suas definições de parâmetro.

## <a name="example"></a>Exemplo

 A seguinte tarefa embutida registra algumas mensagens e retorna uma cadeia de caracteres.

```xml
<Project xmlns='http://schemas.microsoft.com/developer/msbuild/2003' ToolsVersion="15.0">

    <UsingTask TaskName="MySample"
               TaskFactory="RoslynCodeTaskFactory"
               AssemblyFile="$(MSBuildBinPath)\Microsoft.Build.Tasks.Core.dll">
        <ParameterGroup>
            <Parameter1 ParameterType="System.String" Required="true" />
            <Parameter2 ParameterType="System.String" />
            <Parameter3 ParameterType="System.String" Output="true" />
        </ParameterGroup>
        <Task>
            <Using Namespace="System" />
            <Code Type="Fragment" Language="C#">
              <![CDATA[
              Log.LogMessage(MessageImportance.High, "Hello from an inline task created by Roslyn!");
              Log.LogMessageFromText($"Parameter1: '{Parameter1}'", MessageImportance.High);
              Log.LogMessageFromText($"Parameter2: '{Parameter2}'", MessageImportance.High);
              Parameter3 = "A value from the Roslyn CodeTaskFactory";
            ]]>
            </Code>
        </Task>
    </UsingTask>

    <Target Name="Demo">
      <MySample Parameter1="A value for parameter 1" Parameter2="A value for parameter 2">
          <Output TaskParameter="Parameter3" PropertyName="NewProperty" />
      </MySample>

      <Message Text="NewProperty: '$(NewProperty)'" />
    </Target>
</Project>
```

Essas tarefas embutidas podem combinar caminhos e obter o nome do arquivo.

```xml
<Project xmlns='http://schemas.microsoft.com/developer/msbuild/2003' ToolsVersion="15.0">

    <UsingTask TaskName="PathCombine"
               TaskFactory="RoslynCodeTaskFactory"
               AssemblyFile="$(MSBuildBinPath)\Microsoft.Build.Tasks.Core.dll">
        <ParameterGroup>
            <Paths ParameterType="System.String[]" Required="true" />
            <Combined ParameterType="System.String" Output="true" />
        </ParameterGroup>
        <Task>
            <Using Namespace="System" />
            <Code Type="Fragment" Language="C#">
            <![CDATA[
            Combined = Path.Combine(Paths);
            ]]>
            </Code>
        </Task>
    </UsingTask>

    <UsingTask TaskName="PathGetFileName"
             TaskFactory="RoslynCodeTaskFactory"
             AssemblyFile="$(MSBuildBinPath)\Microsoft.Build.Tasks.Core.dll">
        <ParameterGroup>
            <Path ParameterType="System.String" Required="true" />
            <FileName ParameterType="System.String" Output="true" />
        </ParameterGroup>
        <Task>
            <Using Namespace="System" />
            <Code Type="Fragment" Language="C#">
            <![CDATA[
            FileName = System.IO.Path.GetFileName(Path);
            ]]>
            </Code>
        </Task>
    </UsingTask>

    <Target Name="Demo">
        <PathCombine Paths="$(Temp);MyFolder;$([System.Guid]::NewGuid()).txt">
            <Output TaskParameter="Combined" PropertyName="MyCombinedPaths" />
        </PathCombine>

        <Message Text="Combined Paths: '$(MyCombinedPaths)'" />

        <PathGetFileName Path="$(MyCombinedPaths)">
            <Output TaskParameter="FileName" PropertyName="MyFileName" />
        </PathGetFileName>

        <Message Text="File name: '$(MyFileName)'" />
    </Target>
</Project>
```

## <a name="provide-backward-compatibility"></a>Fornecer compatibilidade com versões anteriores

`RoslynCodeTaskFactory`disponibilizado pela primeira vez no MSBuild versão 15,8. Suponha que você tenha uma situação em que deseja dar suporte a versões anteriores do Visual Studio e do MSBuild, quando `RoslynCodeTaskFactory` o não estava disponível, mas `CodeTaskFactory` era, mas você deseja usar o mesmo script de compilação. Você pode usar uma `Choose` construção que usa a `$(MSBuildVersion)` propriedade para decidir no momento da compilação se deseja usar `RoslynCodeTaskFactory` ou retornar para `CodeTaskFactory` , como no exemplo a seguir:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <Choose>
    <When Condition=" '$(MSBuildVersion.Substring(0,2))' >= 16 Or
    ('$(MSBuildVersion.Substring(0,2))' == 15 And '$(MSBuildVersion.Substring(3,1))' >= 8)">
      <PropertyGroup>
        <TaskFactory>RoslynCodeTaskFactory</TaskFactory>
      </PropertyGroup>
    </When>
    <Otherwise>
      <PropertyGroup>
        <TaskFactory>CodeTaskFactory</TaskFactory>
      </PropertyGroup>
    </Otherwise>
  </Choose>
  
  <UsingTask
    TaskName="HelloWorld"
    TaskFactory="$(TaskFactory)"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll">
    <ParameterGroup />
    <Task>
      <Using Namespace="System"/>
      <Using Namespace="System.IO"/>
      <Code Type="Fragment" Language="cs">
        <![CDATA[
         Log.LogError("Using RoslynCodeTaskFactory");
      ]]>
      </Code>
    </Task>
  </UsingTask>

  <Target Name="RunTask" AfterTargets="Build">
    <Message Text="MSBuildVersion: $(MSBuildVersion)"/>
    <Message Text="TaskFactory: $(TaskFactory)"/>
    <HelloWorld />
  </Target>

</Project>
```

## <a name="see-also"></a>Veja também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Passo a passo: Criar uma tarefa embutida](../msbuild/walkthrough-creating-an-inline-task.md)
