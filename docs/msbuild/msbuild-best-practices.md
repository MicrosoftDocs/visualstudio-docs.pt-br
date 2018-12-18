---
title: Práticas recomendadas do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8f32626f02e0381ab285d1d6ae1b3127022da438
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078189"
---
# <a name="msbuild-best-practices"></a>Melhores práticas do MSBuild
Recomendamos as seguintes práticas recomendadas para escrever scripts MSBuild:  
  
-   Os valores de propriedade padrão são mais facilmente tratados usando o atributo `Condition` e não declarando uma propriedade cujo valor padrão pode ser substituído na linha de comando. Por exemplo, use  
  
```xml
<MyProperty Condition="'$(MyProperty)' == ''">
   MyDefaultValue
</MyProperty>
```
  
-   Evite curingas ao selecionar itens. Em vez disso, especifique os arquivos explicitamente. Isso torna mais fácil controlar os erros que podem ocorrer quando você adiciona ou exclui arquivos.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md)
