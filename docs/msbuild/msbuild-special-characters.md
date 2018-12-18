---
title: Caracteres especiais do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- escape characters
- escape
- MSBuild Escape Characters
ms.assetid: 545e6a59-1093-4514-935e-78679a46fb3c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aa1e52e61f4003a9495e1bff5bd64e4edc40a323
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078648"
---
# <a name="msbuild-special-characters"></a>Caracteres especiais do MSBuild
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] reserva alguns caracteres para uso especial em contextos específicos. Você precisa apenas tais caracteres de escape se desejar usá-los literalmente no contexto no qual eles estão reservados. Por exemplo, um asterisco tem um significado especial somente nos atributos `Include` e `Exclude` de uma definição de item e, em chamadas para `CreateItem`. Se você quiser que um asterisco seja exibido como um asterisco em um desses contextos, você deve usar um caractere de escape. Nos outros contextos, basta digitar o asterisco onde você deseja que ele apareça.  
  
 Para fazer o escape de um caractere especial, use a sintaxe %\<xx>, em que \<xx> representa o valor hexadecimal de ASCII do caractere. Para obter mais informações, confira [Como fazer o escape de caracteres especiais no MSBuild](../msbuild/how-to-escape-special-characters-in-msbuild.md).  
  
## <a name="special-characters"></a>Caracteres especiais  
 A tabela a seguir lista os caracteres especiais do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]:  
  
|**Caractere**|**ASCII**|**Uso reservado**|  
|-------------------|---------------|------------------------|  
|%|%25|Metadados de referência|  
|$|%24|Propriedades de referência|  
|@|%40|Listas de Itens de Referência|  
|'|%27|Condições e outras expressões|  
|;|%3B|Separador de lista|  
|?|%3F|Caractere curinga para nomes de arquivos em atributos `Include` e `Exclude`|  
|*|%2A|Caractere curinga para uso em nomes de arquivos em atributos `Include` e `Exclude`|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos avançados](../msbuild/msbuild-advanced-concepts.md)   
 [Itens](../msbuild/msbuild-items.md)