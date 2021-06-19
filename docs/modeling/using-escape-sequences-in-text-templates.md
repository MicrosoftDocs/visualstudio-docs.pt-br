---
title: Usando sequências de escape em modelos de texto
description: Saiba como você pode usar sequências de escape em modelos de texto para gerar marcas de modelo de texto e para escapar caracteres de controle e aspas somente no código C#.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2a3cdabd38f2bf4ef38a31807fabed3ac837b26b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388445"
---
# <a name="use-escape-sequences-in-text-templates"></a>Usar sequências de escape em modelos de texto

Você pode usar sequências de escape em modelos de texto para gerar marcas de modelo de texto e (somente no código C#) para escapar caracteres de controle e aspas.

Para imprimir marcas abertas e fechar para um bloco de código padrão para o arquivo de saída, escape das marcas da seguinte forma:

```
\<# ... \#>
```

Você pode fazer o mesmo com outras diretivas de modelo de texto e marcas de bloco de código.

Se um bloco de texto incluir cadeias de caracteres usadas para escapar marcas de modelo de texto, você poderá usar as seguintes sequências de escape:

- Se uma marca de modelo de texto for precedida por um número par de caracteres de escape ( ), o analisador de modelo incluirá metade dos caracteres de escape e incluirá a sequência como uma marca de modelo \\ de texto. Por exemplo, se houver quatro caracteres de escape no modelo de texto, haverá dois \\ caracteres " " no arquivo gerado.

- Se a marca de modelo de texto for precedida por um número ímpar de caracteres de escape ( ), o analisador de modelo incluirá metade dos caracteres " " mais a própria marca \\ \\ ( \<# or #> ). A marca não é considerada uma marca de modelo de texto.

- Se um caractere de escape ( ) aparecer em qualquer outro lugar em qualquer sequência diferente de onde ele escapa um caractere de controle ou uma aspas (somente em C#), o caractere será \\ produzido diretamente.

## <a name="see-also"></a>Confira também

- [Como gerar modelos a partir de modelos usando sequências de escape](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
