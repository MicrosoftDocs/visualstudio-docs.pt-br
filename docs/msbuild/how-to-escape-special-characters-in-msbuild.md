---
title: Como escapar caracteres especiais no MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- special characters, escaping
- characters, escapes
- escape characters
- MSBuild, escaping special characters
ms.assetid: 1aa3669c-1647-4960-b770-752e2532102f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 701db598872f6dde5a07740ef7601a6c8de7c5f0
ms.sourcegitcommit: 6672a1e9d135d7e5cca3cceea07c6fe5a0871475
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47443396"
---
# <a name="how-to-escape-special-characters-in-msbuild"></a>Como fazer o escape de caracteres especiais no MSBuild

Determinados caracteres têm significado especial em arquivos de projeto do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. O ponto-e-vírgula (`;`) e os asteriscos (`*`) são exemplos de caracteres. Para obter uma lista completa desses caracteres especiais, confira [Caracteres especiais do MSBuild](../msbuild/msbuild-special-characters.md).
  
Para usar esses caracteres especiais como literais em um arquivo de projeto, eles precisam ser especificados com a sintaxe `%<xx>`, em que `<xx>` representa o valor hexadecimal ASCII do caractere.
  
## <a name="msbuild-special-characters"></a>Caracteres especiais do MSBuild

 Um exemplo de quando os caracteres especiais são usados é no atributo `Include` de listas de itens. Por exemplo, a seguinte lista de itens declara dois itens: *MyFile.cs* e *MyClass.cs*.  
  
```xml  
<Compile Include="MyFile.cs;MyClass.cs"/>  
```  
  
Caso deseje declarar um item que contém um ponto e vírgula no nome, use a sintaxe `%<xx>` para fazer o escape do ponto e vírgula e impedir que o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] declare dois itens separados. Por exemplo, o item a seguir escapa o ponto e vírgula e declara um item denominado `MyFile.cs;MyClass.cs`.
  
```xml  
<Compile Include="MyFile.cs%3BMyClass.cs"/>  
```  

Também é possível usar uma [função de propriedade](../msbuild/property-functions.md) para fazer o escape de cadeias de caracteres. Por exemplo, isso equivale ao exemplo anterior.

```xml
<Compile Include="$([MSBuild]::Escape('MyFile.cs;MyClass.cs'))" />
```

### <a name="to-use-an-msbuild-special-character-as-a-literal-character"></a>Para usar um caractere especial do MSBuild como um caractere literal

Use a notação `%<xx>` no lugar do caractere especial, em que `<xx>` representa o valor hexadecimal do caractere ASCII. Por exemplo, para usar um asterisco (`*`) como um caractere literal, use o valor `%2A`.

 
## <a name="see-also"></a>Consulte também  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [MSBuild](../msbuild/msbuild.md)   
 [Itens](../msbuild/msbuild-items.md)   
