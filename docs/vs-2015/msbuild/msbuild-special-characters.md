---
title: Caracteres especiais do MSBuild | Microsoft Docs
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
- escape characters
- escape
- MSBuild Escape Characters
ms.assetid: 545e6a59-1093-4514-935e-78679a46fb3c
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0c9ce1697f370ec1beec8ce12faceb15825fbe5f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49256438"
---
# <a name="msbuild-special-characters"></a>Caracteres especiais no MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] reserva alguns caracteres para uso especial em contextos específicos. Você precisa apenas tais caracteres de escape se desejar usá-los literalmente no contexto no qual eles estão reservados. Por exemplo, um asterisco tem um significado especial somente nos atributos `Include` e `Exclude` de uma definição de item e, em chamadas para `CreateItem`. Se você quiser que um asterisco seja exibido como um asterisco em um desses contextos, você deve usar um caractere de escape. Nos outros contextos, basta digitar o asterisco onde você deseja que ele apareça.  
  
 Para escapar um caractere especial, use a sintaxe %*xx*, onde *xx* representa o valor hexadecimal de ASCII do caractere. Para obter mais informações, confira [Como: usar caracteres especiais no MSBuild](../msbuild/how-to-escape-special-characters-in-msbuild.md).  
  
## <a name="special-characters"></a>Caracteres especiais  
 A tabela a seguir lista os caracteres especiais do [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]:  
  
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



