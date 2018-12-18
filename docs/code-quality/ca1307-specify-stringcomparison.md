---
title: 'CA1307: especificar StringComparison'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1307
- SpecifyStringComparison
helpviewer_keywords:
- CA1307
- SpecifyStringComparison
ms.assetid: 9b0d5e71-1683-4a0d-bc4a-68b2fbd8af71
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 67f0d5152dcdef5ffa3abb76d92e68fd99f9b637
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550408"
---
# <a name="ca1307-specify-stringcomparison"></a>CA1307: especificar StringComparison

|||
|-|-|
|NomeDoTipo|SpecifyStringComparison|
|CheckId|CA1307|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma operação de comparação de cadeia de caracteres usa uma sobrecarga de método não define uma <xref:System.StringComparison> parâmetro.

## <a name="rule-description"></a>Descrição da regra
 Muitas operações, mais importante da cadeia de caracteres a <xref:System.String.Compare%2A> e <xref:System.String.Equals%2A> métodos, fornecer uma sobrecarga que aceita um <xref:System.StringComparison> valor de enumeração como um parâmetro.

 Sempre que uma sobrecarga existe que utiliza um <xref:System.StringComparison> parâmetro, ele deve ser usado em vez de uma sobrecarga que não utilize esse parâmetro. Definindo explicitamente esse parâmetro, seu código é geralmente feita mais clara e fácil de manter.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, altere métodos de comparação de cadeia de caracteres para sobrecargas que aceitam o <xref:System.StringComparison> enumeração como um parâmetro. Por exemplo: altere `String.Compare(str1, str2)` para `String.Compare(str1, str2, StringComparison.Ordinal)`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, quando a biblioteca ou o aplicativo é destinado a um público limitado de local e, portanto, não será localizado.

## <a name="see-also"></a>Consulte também

- [Avisos de globalização](../code-quality/globalization-warnings.md)
- [CA1309: usar StringComparison ordinal](../code-quality/ca1309-use-ordinal-stringcomparison.md)