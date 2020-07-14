---
title: Condições do MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, conditions
- conditions [MSBuild]
- Exists, MSBuild condition function
- HasTrailingSlash, MSBuild condition function
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fea7763bf1cbce5fac36ce2cd5e54c40e1da989a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289229"
---
# <a name="msbuild-conditions"></a>Condições do MSBuild

O MSBuild dá suporte a um conjunto específico de condições que podem ser aplicadas sempre que um `Condition` atributo é permitido. A tabela a seguir explica essas condições.

|Condição|Descrição|
|---------------|-----------------|
|'`stringA`' == '`stringB`'|Avaliará como `true` se `stringA` for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(Configuration)'=='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios. Essa verificação não diferencia maiúsculas de minúsculas.|
|'`stringA`' != '`stringB`'|Avaliará como `true` se `stringA` não for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(Configuration)'!='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios. Essa verificação não diferencia maiúsculas de minúsculas.|
|\<, >, \<=, >=|Avalia os valores numéricos dos operandos. Retornará `true` se a avaliação relacional for true. Os operandos devem ser avaliados como um número decimal ou hexadecimal. Os números hexadecimais devem começar com "0x". **Observação:** no XML, os caracteres `<` e `>` devem ser escapados. O símbolo `<` é representado como `&lt;`. O símbolo `>` é representado como `&gt;`.|
|Exists('`stringA`')|Avaliará como `true` se existir um arquivo ou pasta com o nome `stringA`.<br /><br /> Por exemplo:<br /><br /> `Condition="!Exists('$(Folder)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|
|HasTrailingSlash('`stringA`')|Avaliará como `true` se a cadeia de caracteres contiver um caractere de barra invertida (\\) ou de barra "/" à direita.<br /><br /> Por exemplo:<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|
|!|Avaliará como `true` se o operando for avaliado como `false`.|
|`And`|Avaliará como `true` se ambos os operandos forem avaliados como `true`.|
|`Or`|Avaliará como `true` se pelo menos um dos operandos for avaliado como `true`.|
|()|Mecanismo de agrupamento que será avaliado como `true` se as expressões contidas dentro forem avaliadas como `true`.|
|$if$ ( %expression% ), $else$, $endif$|Verifica se o `%expression%` especificado corresponde ao valor de cadeia de caracteres do parâmetro do modelo personalizado passado. Se a condição `$if$` for avaliada como `true`, suas declarações serão executadas, caso contrário, a condição `$else$` será verificada. Se a condição `$else$` for `true`, suas declarações serão executadas, caso contrário, a condição `$endif$` encerrará a avaliação da expressão.<br /><br /> Para obter exemplos de uso, consulte [lógica de parâmetro de modelo de projeto/item do Visual Studio](https://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic).|

Você pode usar métodos de cadeia de caracteres em condições, conforme mostrado no exemplo a seguir, no qual a função [TrimEnd ()](/dotnet/api/system.string.trimend) é usada para comparar apenas a parte relevante da cadeia de caracteres, para diferenciar entre .NET Framework e estruturas de destino do .NET Core.

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFrameworks>net45;net48;netstandard2.1;netcoreapp2.1;netcoreapp3.1</TargetFrameworks>
    </PropertyGroup>

    <PropertyGroup Condition="'$(TargetFramework.TrimEnd(`0123456789`))' == 'net'">
        <!-- Properties for .NET Framework -->
    </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Veja também

- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Construções condicionais](../msbuild/msbuild-conditional-constructs.md)
- [Walkthrough: Criando um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)
