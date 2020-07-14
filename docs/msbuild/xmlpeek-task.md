---
title: Tarefa XmlPeek | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XmlPeek task [MSBuild]
- MSBuild, XmlPeek task
ms.assetid: 19196031-a3bc-41b5-9c4a-f2572630e179
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27b535af260d205c74ef87d0325680389d1dbe58
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286110"
---
# <a name="xmlpeek-task"></a>Tarefa XmlPeek

Retorna os valores conforme especificado por uma consulta de XPath em um arquivo XML.

## <a name="parameters"></a>Parâmetros

 A tabela a seguir descreve os parâmetros da tarefa `XmlPeek`.

|Parâmetro|Descrição|
|---------------|-----------------|
|`Namespaces`|Parâmetro `String` opcional.<br /><br /> Especifica os namespaces para prefixos de consulta do XPath.|
|`Query`|Parâmetro `String` opcional.<br /><br /> Especifica a consulta do XPath.|
|`Result`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém os resultados que são retornados por essa tarefa.|
|`XmlContent`|Parâmetro `String` opcional.<br /><br /> Especifica a entrada XML como uma cadeia de caracteres.|
|`XmlInputPath`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica a entrada XML como um caminho de arquivo.|

## <a name="remarks"></a>Comentários

 Além de ter os parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).

## <a name="example"></a>Exemplo

Aqui está um arquivo XML `settings.config` de exemplo para ler:

```xml
<appSettings>
  <add key="ProjectFolder" value="S1" />
</appSettings>
```

Neste exemplo, se você quiser ler `value` , use um código semelhante ao seguinte:

```xml
<Target Name="BeforeBuild">
    <XmlPeek XmlInputPath="settings.config" Query="appSettings/add[@key='ProjectFolder']/@value">
        <Output TaskParameter="Result" ItemName="value" />
    </XmlPeek>
    <Message Text="Using project folder @(value)." Importance="high" />
    <PropertyGroup>
        <ProjectFolder>@(value)</ProjectFolder>
    </PropertyGroup>
    <ItemGroup>
        <Compile Include="Projects\$(ProjectFolder)\Controls\Control1.ascx.cs">
            <SubType>ASPXCodeBehind</SubType>
        </Compile>
    </ItemGroup>
</Target>
```

Com namespaces XML, você usa o `Namespaces` parâmetro, como no exemplo a seguir. Com o arquivo XML de entrada `XMLFile1.xml` :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<class AccessModifier='public' Name='test' xmlns:s='http://nsurl'>
  <s:variable Type='String' Name='a'>This</s:variable>
  <s:variable Type='String' Name='b'>is</s:variable>
  <s:variable Type='String' Name='c'>Sparta!</s:variable>
  <method AccessModifier='public static' Name='GetVal' />
</class>
```

E o seguinte `Target` definido em um arquivo de projeto:

```xml
  <Target Name="TestPeek" BeforeTargets="Build">
    <!-- Find the Name attributes -->
    <XmlPeek XmlInputPath="XMLFile1.xml"
             Query="//s:variable/@Name"
             Namespaces="&lt;Namespace Prefix='s' Uri='http://nsurl' /&gt;">
      <Output TaskParameter="Result" ItemName="value1" />
    </XmlPeek>
    <Message Text="@(value1)"/>
    <!-- Find 'variable' nodes (XPath query includes ".") -->
    <XmlPeek XmlInputPath="XMLFile1.xml"
             Query="//s:variable/."
             Namespaces="&lt;Namespace Prefix='s' Uri='http://nsurl' /&gt;">
      <Output TaskParameter="Result" ItemName="value2" />
    </XmlPeek>
    <Message Text="@(value2)"/>
  </Target>
```

A saída inclui o seguinte do `TestPeek` destino:

```output
  TestPeek output:
  a;b;c
  <s:variable Type="String" Name="a" xmlns:s="http://nsurl">This</s:variable>;<s:variable Type="String" Name="b" xmlns:s="http://nsurl">is</s:variable>;<s:variable Type="String" Name="c" xmlns:s="http://nsurl">Sparta!</s:variable>
```

## <a name="see-also"></a>Veja também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefa](../msbuild/msbuild-task-reference.md)
- [Sintaxe de consulta XPath](https://wikipedia.org/wiki/XPath)
