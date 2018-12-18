---
title: Práticas recomendadas do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- best practices, MSBuild
- MSBuild, best practices
ms.assetid: 90ef8693-e921-410a-a377-fe4d13f58c48
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94941cacdfea79c2d846b9936b8532f155d6cebb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49218381"
---
# <a name="msbuild-best-practices"></a>Práticas recomendadas do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Recomendamos as seguintes práticas recomendadas para escrever scripts MSBuild:  
  
-   Os valores de propriedade padrão são mais facilmente tratados usando o atributo `Condition` e não declarando uma propriedade cujo valor padrão pode ser substituído na linha de comando. Por exemplo, use  
  
     `<MyProperty Condition="$(MyProperty)" == ''>`  
  
     `MyDefaultValue`  
  
     `</MyProperty>`  
  
-   Evite curingas ao selecionar itens. Em vez disso, especifique os arquivos explicitamente. Isso torna mais fácil controlar os erros que podem ocorrer quando você adiciona ou exclui arquivos.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md)



