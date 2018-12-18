---
title: Usando sequências de Escape em modelos de texto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text templates, escape sequences
ms.assetid: 36fff542-2f42-460f-a2d5-03fc76817f3b
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: be273c8cf69094a640ea7210bdbdc50005841a49
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49296530"
---
# <a name="using-escape-sequences-in-text-templates"></a>Usando sequências de escape em modelos de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar sequências de escape em modelos de texto para gerar marcações de modelo de texto e (no c# somente código) para caracteres de controle de escape e aspas.  
  
 Para imprimir as marcas de abertura e fechamento de um bloco de código padrão para o arquivo de saída, escape as marcas da seguinte maneira:  
  
```  
\<# ... \#>  
```  
  
 Você pode fazer o mesmo com marcas de bloco outro texto modelo diretiva e código.  
  
 Se um bloco de texto inclui cadeias de caracteres usadas para sair de marcas do modelo de texto, em seguida, você pode usar as seguintes sequências de escape:  
  
-   Se uma marca de modelo de texto é precedida por um número par de escape (\\) caracteres o modelo de analisador será incluir metade dos caracteres de escape e a sequência como uma marca de modelo de texto. Por exemplo, se houver quatro caracteres de escape no modelo de texto, haverá dois "\\" caracteres no arquivo gerado.  
  
-   Se a marcação de modelo de texto é precedida por um número ímpar de escape (\\) caracteres, o analisador de modelo incluirá metade da "\\" caracteres além de marca em si (\<# ou #>). A marca não é considerada uma marca de modelo de texto.  
  
-   Se um escape (\\) caracteres é exibida em qualquer lugar em qualquer sequência diferente de onde ele realiza o escape de um caractere de controle ou uma cotação (no c# somente), o caractere será gerado diretamente.  
  
## <a name="see-also"></a>Consulte também  
 [Como gerar modelos com base em modelos usando sequências de escape](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)



