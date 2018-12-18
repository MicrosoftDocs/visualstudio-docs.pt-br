---
title: Condições do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, conditions
- conditions [MSBuild]
ms.assetid: 9d7aa308-b667-48ed-b4c9-a61e49eb0a85
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 64c1ac7eb3f90444da702d699201a251aaba411c
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39077585"
---
# <a name="msbuild-conditions"></a>Condições do MSBuild
O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] dá suporte a um conjunto de condições específico que pode ser aplicado sempre que um atributo `Condition` é permitido. A tabela a seguir explica essas condições.  
  
|Condição|Descrição|  
|---------------|-----------------|  
|'`stringA`' == '`stringB`'|Avaliará como `true` se `stringA` for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(CONFIG)'=='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|  
|'`stringA`' != '`stringB`'|Avaliará como `true` se `stringA` não for igual a `stringB`.<br /><br /> Por exemplo:<br /><br /> `Condition="'$(CONFIG)'!='DEBUG'"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|  
|\<, >, \<=, >=|Avalia os valores numéricos dos operandos. Retornará `true` se a avaliação relacional for true. Os operandos devem ser avaliados como um número decimal ou hexadecimal. Os números hexadecimais devem começar com "0x". **Observação:** no XML, os caracteres `<` e `>` devem ser escapados. O símbolo `<` é representado como `&lt;`. O símbolo `>` é representado como `&gt;`.|  
|Exists('`stringA`')|Avaliará como `true` se existir um arquivo ou pasta com o nome `stringA`.<br /><br /> Por exemplo:<br /><br /> `Condition="!Exists('$(builtdir)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|  
|HasTrailingSlash('`stringA`')|Avaliará como `true` se a cadeia de caracteres contiver um caractere de barra invertida (\\) ou de barra "/" à direita.<br /><br /> Por exemplo:<br /><br /> `Condition="!HasTrailingSlash('$(OutputPath)')"`<br /><br /> As aspas simples não são necessárias para cadeias de caracteres alfanuméricas simples ou valores boolianos. No entanto, as aspas são necessárias para valores vazios.|  
|!|Avaliará como `true` se o operando for avaliado como `false`.|  
|And|Avaliará como `true` se ambos os operandos forem avaliados como `true`.|  
|Ou|Avaliará como `true` se pelo menos um dos operandos for avaliado como `true`.|  
|()|Mecanismo de agrupamento que será avaliado como `true` se as expressões contidas dentro forem avaliadas como `true`.|  
|$if$ ( %expression% ), $else$, $endif$|Verifica se o `%expression%` especificado corresponde ao valor de cadeia de caracteres do parâmetro do modelo personalizado passado. Se a condição `$if$` for avaliada como `true`, suas declarações serão executadas, caso contrário, a condição `$else$` será verificada. Se a condição `$else$` for `true`, suas declarações serão executadas, caso contrário, a condição `$endif$` encerrará a avaliação da expressão.<br /><br /> Para obter exemplos de uso, confira [Lógica de parâmetro do modelo de item/projeto do Visual Studio](http://stackoverflow.com/questions/6709057/visual-studio-project-item-template-parameter-logic).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Constructos condicionais](../msbuild/msbuild-conditional-constructs.md)   
 [Passo a passo: Criando um arquivo de projeto do MSBuild do zero](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)
