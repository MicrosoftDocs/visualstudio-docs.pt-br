---
title: Diretiva de assembly T4
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: cd7f1f36374f3411b5a76f5df5e3e25bb52df230
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948625"
---
# <a name="t4-assembly-directive"></a>Diretiva de assembly T4

Em um modelo de texto de tempo de design do Visual Studio, o `assembly` diretiva carrega um assembly para que o código de modelo possa usar seus tipos. O efeito é semelhante a adicionar uma referência de assembly em um projeto do Visual Studio.

 Para obter uma visão geral da gravação de modelos de texto, consulte [gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md).

> [!NOTE]
>  Você não precisa da diretiva `assembly` em um modelo de texto de tempo de execução (pré-processado). Em vez disso, adicione os assemblies necessários para o **referências** do projeto do Visual Studio.

## <a name="using-the-assembly-directive"></a>Usando a diretiva de assembly
 A sintaxe da diretiva é a seguinte:

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

 O nome do assembly deve ser um dos seguintes:

- O nome forte do assembly no GAC, como `System.Xml.dll`. Você também pode usar o formato longo, como `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"`. Para obter mais informações, consulte <xref:System.Reflection.AssemblyName>.

- O caminho absoluto do assembly

  Você pode usar o `$(variableName)` sintaxe para fazer referência a variáveis do Visual Studio, como `$(SolutionDir)`, e `%VariableName%` para referenciar variáveis de ambiente. Por exemplo:

```
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>
```

 A diretiva de assembly não tem nenhum efeito em um modelo de texto pré-processado. Em vez disso, inclui as referências necessárias na **referências** seção de seu projeto do Visual Studio. Para obter mais informações, consulte [geração de texto de tempo de execução com modelos de texto T4](../modeling/run-time-text-generation-with-t4-text-templates.md).

## <a name="standard-assemblies"></a>Assemblies padrão
 Os seguintes assemblies são carregados automaticamente, de modo que não seja necessário gravar diretivas de assembly para eles:

- `Microsoft.VisualStudio.TextTemplating.1*.dll`

- `System.dll`

- `WindowsBase.dll`

  Se você usar uma diretiva personalizada, o processador de diretriz pode carregar os assemblies adicionais. Por exemplo, se você gravar modelos para uma linguagem específica do domínio (DSL), você não precisa gravar diretivas de assembly para os assemblies a seguir:

- `Microsoft.VisualStudio.Modeling.Sdk.1*.dll`

- `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.1*.dsl`

- `Microsoft.VisualStudio.TextTemplating.Modeling.1*.dll`

- O assembly que contém seu DSL.

## <a name="msbuild"></a> Usando propriedades do projeto no MSBuild e o Visual Studio
 Macros do Visual Studio como $ (solutiondir) não funcionam no MSBuild. Se você quiser transformar modelos no computador de compilação, use as propriedades do projeto como alternativa.

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

 Agora você pode usar a propriedade do projeto em modelos de texto, que se transformam corretamente no Visual Studio e no MSBuild:

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
```

## <a name="see-also"></a>Consulte também

- [Diretiva de inclusão T4](../modeling/t4-include-directive.md)