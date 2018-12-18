---
title: Usando sequências de escape em modelos de texto
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: b8e92a4bbd149d96b6db710daf32dc72024d57da
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31950381"
---
# <a name="using-escape-sequences-in-text-templates"></a>Usando sequências de escape em modelos de texto
Você pode usar sequências de escape em modelos de texto para gerar marcas de modelo de texto e (em c# somente código) para caracteres de controle de escape e aspas.

 Para imprimir marcas de abertura e fechamento de um bloco de código padrão para o arquivo de saída, retirar as marcas da seguinte maneira:

```
\<# ... \#>
```

 Você pode fazer o mesmo com marcas de bloco outro texto modelo diretiva e código.

 Se um bloco de texto incluem cadeias de caracteres usadas para sair de marcas de modelo de texto, você pode usar sequências de escape a seguir:

-   Se uma marca de modelo de texto é precedida por um número par de escape (\\) caracteres o modelo de analisador será inclui metade dos caracteres de escape e inclui a sequência como uma marca de modelo de texto. Por exemplo, se houver quatro caracteres de escape no modelo de texto, haverá dois "\\" caracteres no arquivo gerado.

-   Se a marca de modelo de texto é precedida por um número ímpar de escape (\\) caracteres, o analisador de modelo incluirá metade do "\\" caracteres e a própria marca (\<# ou #>). A marca não é considerada para ser uma marca de modelo de texto.

-   Se um escape (\\) caractere aparece em qualquer lugar em qualquer sequência diferente de onde ela ignora a um caractere de controle ou (em c# somente), o caractere será saído diretamente.

## <a name="see-also"></a>Consulte também

- [Como gerar modelos com base em modelos usando sequências de escape](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)