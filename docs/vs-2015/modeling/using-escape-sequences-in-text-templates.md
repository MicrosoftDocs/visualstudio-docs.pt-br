---
title: Usando sequências de Escape em modelos de texto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
ms.assetid: 36fff542-2f42-460f-a2d5-03fc76817f3b
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: aecd53f9321108d429c732cc8b802ee5dfc8a99c
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58922712"
---
# <a name="using-escape-sequences-in-text-templates"></a>Usando sequências de escape em modelos de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar sequências de escape em modelos de texto para gerar marcações de modelo de texto e (no C# somente código) para caracteres de controle de escape e aspas.  
  
 Para imprimir as marcas de abertura e fechamento de um bloco de código padrão para o arquivo de saída, escape as marcas da seguinte maneira:  
  
```  
\<# ... \#>  
```  
  
 Você pode fazer o mesmo com marcas de bloco outro texto modelo diretiva e código.  
  
 Se um bloco de texto inclui cadeias de caracteres usadas para sair de marcas do modelo de texto, em seguida, você pode usar as seguintes sequências de escape:  
  
-   Se uma marca de modelo de texto é precedida por um número par de escape (\\) caracteres o modelo de analisador será incluir metade dos caracteres de escape e a sequência como uma marca de modelo de texto. Por exemplo, se houver quatro caracteres de escape no modelo de texto, haverá dois "\\" caracteres no arquivo gerado.  
  
-   Se a marcação de modelo de texto é precedida por um número ímpar de escape (\\) caracteres, o analisador de modelo incluirá metade da "\\" caracteres além de marca em si (\<# ou #>). A marca não é considerada uma marca de modelo de texto.  
  
-   Se um escape (\\) caracteres é exibida em qualquer lugar em qualquer sequência diferente de onde ele realiza o escape de um caractere de controle ou uma cotação (no C# somente), o caractere será gerado diretamente.  
  
## <a name="see-also"></a>Consulte também  
 [Como: Gerar modelos com base em modelos usando sequências de escape](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
