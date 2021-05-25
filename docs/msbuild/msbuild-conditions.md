---
title: Condições do MSBuild | Microsoft Docs
description: Saiba como o MSBuild dá suporte a um conjunto específico de condições que podem ser aplicadas sempre que um atributo Condition é permitido.
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 76bafaf5192c59e0f23078e396ae553b3023e060
ms.sourcegitcommit: d3577395cf016f2836eb5a3c1d496cca6d449baa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2021
ms.locfileid: "110413319"
---
# <a name="msbuild-conditions"></a>Condições do MSBuild

O MSBuild dá suporte a um conjunto específico de condições que podem ser aplicadas sempre que um `Condition` atributo é permitido. A tabela a seguir explica essas condições.

|Condição|Descrição|
|---------------|-----------------|
|'`stringA`' == '`stringB`'|Avaliará como `true` se `stringA` for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(Configuration)'=='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios. Essa verificação não faz sentido para maiúsculas e minúsculas.|
|'`stringA`' != '`stringB`'|Avaliará como `true` se `stringA` não for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(Configuration)'!='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios. Essa verificação não faz sentido para maiúsculas e minúsculas.|
|\<, >, \<=, >=|Avalia os valores numéricos dos operandos. Retornará `true` se a avaliação relacional for true. Os operadores devem ser avaliado como um número decimal ou hexadecimal ou uma versão pontilhada de quatro partes. Os números hexadecimais devem começar com "0x". **Observação:** no XML, os caracteres `<` e `>` devem ser escapados. O símbolo `<` é representado como `&lt;`. O símbolo `>` é representado como `&gt;`.|
|Exists('`stringA`')|Avaliará como `true` se existir um arquivo ou pasta com o nome `stringA`.<br /><br /> Por exemplo:<br /><br /> `Condition="!Exists('$(Folder)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|
|HasTrailingSlash('`stringA`')|Avaliará como `true` se a cadeia de caracteres contiver um caractere de barra invertida (\\) ou de barra "/" à direita.<br /><br /> Por exemplo:<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|
|!|Avaliará como `true` se o operando for avaliado como `false`.|
|`And`|Avaliará como `true` se ambos os operandos forem avaliados como `true`.|
|`Or`|Avaliará como `true` se pelo menos um dos operandos for avaliado como `true`.|
|()|Mecanismo de agrupamento que será avaliado como `true` se as expressões contidas dentro forem avaliadas como `true`.|
|$if$ ( %expression% ), $else$, $endif$|Verifica se o `%expression%` especificado corresponde ao valor de cadeia de caracteres do parâmetro do modelo personalizado passado. Se a condição `$if$` for avaliada como `true`, suas declarações serão executadas, caso contrário, a condição `$else$` será verificada. Se a condição `$else$` for `true`, suas declarações serão executadas, caso contrário, a condição `$endif$` encerrará a avaliação da expressão.<br /><br /> Para ver exemplos de uso, consulte Visual Studio lógica do parâmetro de [modelo de projeto/item](https://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic).|

Você pode usar métodos de cadeia de caracteres em condições, conforme mostrado no exemplo a seguir, no qual a [função TrimEnd()](/dotnet/api/system.string.trimend) é usada para comparar apenas a parte relevante da cadeia de caracteres, para diferenciar entre as estruturas de destino .NET Framework e .NET Core.

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

Em arquivos de projeto do MSBuild, não há nenhum tipo booliana verdadeiro. Os dados boolianas são representados em propriedades que podem estar vazias ou definidas como qualquer valor. Portanto, `'$(Prop)' == 'true'` significa "se Prop for `true` ,", mas `'$(Prop)' != 'false'` significa "se Prop for ou `true` desa definir para outra coisa".

A lógica booliana só é avaliada no contexto de condições, portanto, as configurações de propriedade como são representadas como uma cadeia de caracteres (após a expansão da variável), não avaliadas como `<Prop2>'$(Prop1)' == 'true'</Prop>` valores boolianas.  

O MSBuild implementa algumas regras de processamento especiais para facilitar o trabalho com propriedades de cadeia de caracteres que são usadas como valores boolianas. Literais boolianas são aceitos e funcionam `Condition="true"` `Condition="false"` conforme o esperado. O MSBuild também inclui regras especiais para dar suporte ao operador de negação booliana. Portanto, se `$(Prop)` for 'true', `!$(Prop)` expandirá para `!true` e isso será comparado como , como você `false` esperaria.

## <a name="comparing-versions"></a>Comparando versões

Os operadores relacionais , , e suportam versões, conforme analisado por , para que você possa comparar versões que têm quatro partes numéricas `<` `>` entre `<=` `>=` <xref:System.Version?displayProperty=fullName> si. Por exemplo, `'1.2.3.4' < '1.10.0.0'` é `true` .

> [!CAUTION]
> `System.Version` as comparações podem produzir resultados surpreendentes quando uma ou ambas as versões não especificam todas as quatro partes. Por exemplo, a versão 1.1 é anterior à versão 1.1.0.

O MSBuild fornece [funções de propriedade para comparar versões](property-functions.md#MSBuild-version-comparison-functions) que têm um conjunto diferente de regras compatíveis com o controle de versão semântico (semver).

## <a name="see-also"></a>Confira também

- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Construções condicionais](../msbuild/msbuild-conditional-constructs.md)
- [Passo a passo: Criar um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)
